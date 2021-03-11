<template>
  <div class="home">
    <FilterNav
      @filterChange="currentFilter = $event"
      :currentFilter="currentFilter"
    />

    <ul v-if="filteredProjects.length">
      <li
        class="list-item"
        v-for="project in filteredProjects"
        :key="project.id"
      >
        <ProjectItem
          :project="project"
          @delete="handleDelete"
          @toggleCompleted="handleToggleCompleted"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import ProjectItem from "../components/ProjectItem.vue";
import FilterNav from "../components/FilterNav.vue";

export default {
  name: "Home",
  components: { ProjectItem, FilterNav },
  data() {
    return {
      projects: [],
      currentFilter: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(projectId) {
      this.projects = this.projects.filter((p) => p.id !== projectId);
    },
    handleToggleCompleted(projectId) {
      this.projects = this.projects.map((p) => {
        if (p.id === projectId) {
          return { ...p, completed: !p.completed };
        }
        return p;
      });
    },
  },
  computed: {
    filteredProjects() {
      if (this.currentFilter === "completed")
        return this.projects.filter((p) => p.completed);

      if (this.currentFilter === "ongoing")
        return this.projects.filter((p) => !p.completed);

      return this.projects;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
.list-item {
  list-style-type: none;
}
</style>
