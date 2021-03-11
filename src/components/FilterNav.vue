<template>
  <nav class="filter-nav">
    <button :class="{ active: currentFilter === 'all' }" @click="setFilter('all')">
      View All
    </button>

    <button
      :class="{ active: currentFilter === 'completed' }"
      @click="setFilter('completed')"
    >
      Completed
    </button>

    <button
      :class="{ active: currentFilter === 'ongoing' }"
      @click="setFilter('ongoing')"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["currentFilter"],
  methods: {
    setFilter(filterBy) {
      this.$emit("filterChange", filterBy);
    },
  },
};
</script>

<style>
.filter-nav {
  text-align: center;
}
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  cursor: pointer;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
  margin-right: 10px;
  outline: none;
  text-transform: uppercase;
}
.filter-nav button.active {
  color: #555;
}
</style>
