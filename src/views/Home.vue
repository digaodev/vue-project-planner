<template>
  <div class="home">
    <ul v-if="projects.length">
      <li class="list-item" v-for="project in projects" :key="project.id">
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

export default {
  name: "Home",
  components: { ProjectItem },
  data() {
    return {
      projects: [],
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
          return {...p, completed: !p.completed}
        }
        return p
      });
    },
  },
};
</script>

<style scoped>
.list-item {
  list-style-type: none;
}
</style>
