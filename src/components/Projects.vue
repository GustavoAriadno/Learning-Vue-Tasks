<template>
  <div>
    <h3>Projects</h3>
    <ul class="list">
      <li @click="emitFilter('')">(All)</li>
      <li
        v-for="project in projects"
        :key="project"
        @click="emitFilter(project)"
      >
        {{ project | upper }}
      </li>
    </ul>
    <input
      type="text"
      placeholder="Add a project"
      maxlength="20"
      v-model="newProject"
      v-on:keyup.enter="emitNewProject"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      newProject: "",
    };
  },

  props: {
    projects: Array,
  },

  methods: {
    emitNewProject: function () {
      if (this.newProject.trim().length >= 3)
        this.$emit("newProject", { newProject: this.newProject.trim() });
      this.newProject = "";
    },

    emitFilter: function (selectedFilter) {
      this.$emit("newFilter", { selectedFilter });
    },
  },

  filters: {
    upper: function (value) {
      if (value == "") return;
      return `${value[0].toUpperCase()}${value.slice(1)}`;
    },
  },
};
</script>

<style>
h3 {
  color: #ffffff;
  padding: 0.5rem;
  margin: 1rem;
  font-weight: bolder;
}

.list {
  cursor: pointer;
}
</style>