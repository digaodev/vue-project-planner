<template>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title:</label>
    <input type="text" id="title" name="title" required v-model="title" />

    <label for="details">Details:</label>
    <textarea name="details" id="details" required v-model="details"></textarea>

    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
        completed: false,
      };

      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(project),
      })
        .then(() => this.$router.push('/'))
        .catch(err => console.log(err.message))
    },
  },
};
</script>

<style>
form {
  background: #fff;
  border-radius: 10px;
  padding: 20px;
}

label {
  display: block;

  color: #777;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
  text-transform: uppercase;
}

input {
  border: 0;
  border-bottom: 1px solid #ccc;
  margin-bottom: 24px;
  padding: 10px;
  width: 100%;
}

textarea {
  border: 1px solid #ccc;
  height: 100px;
  padding: 10px;
  width: 100%;
}

form button {
  display: block;

  background: #00ce89;
  border: 0;
  border-radius: 6px;
  color: #fff;
  font-size: 16px;
  font-weight: bold;
  margin: 20px auto 0;
  padding: 10px 20px;
}
</style>
