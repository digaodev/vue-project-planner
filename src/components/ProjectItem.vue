<template>
  <div class="project" :class="{ completed: project.completed }">
    <div class="actions">
      <h3 @click="toggleIsShowing">{{ project.title }}</h3>

      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons">edit</span>
        </router-link>
        <span class="material-icons tick" @click="toggleCompletedProject"
          >done</span
        >
        <span class="material-icons" @click="deleteProject">delete</span>
      </div>
    </div>

    <div class="details" v-if="isShowing">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      isShowing: false,
      uri: `http://localhost:3000/projects/${this.project.id}`,
    };
  },
  methods: {
    toggleIsShowing() {
      this.isShowing = !this.isShowing;
    },
    deleteProject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project.id))
        .catch((err) => console.log(err.message));
    },
    toggleCompletedProject() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ completed: !this.project.completed }),
      })
        .then(() => this.$emit("toggleCompleted", this.project.id))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style scoped>
.project {
  background: #fff;
  border-left: 4px solid #e90074;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  margin: 20px auto;
  padding: 10px 20px;
}

h3 {
  cursor: pointer;
}

.actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.material-icons {
  color: #bbb;
  cursor: pointer;
  font-size: 24px;
  margin-left: 10px;
}

.material-icons:hover {
  color: #777;
}

.project.completed {
  border-left: 4px solid #00ce89;
}

.project.completed .tick {
  color: #00ce89;
}
</style>
