<template>
  <div>
    <form class="my-form" v-on:submit.prevent>
      <input type="text" placeholder="Title" maxlength="20" v-model="title" />
      <textarea
        placeholder="Description"
        maxlength="150"
        v-model="description"
      />
      <select v-model="selectedProject">
        <option value="">Select a project</option>
        <option v-for="project in projects" :key="project">
          {{ project }}
        </option>
      </select>
      <button class="form-button" @click="emitNewTask">Save</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
      selectedProject: "",
    };
  },

  props: {
    id: Number,
    projects: Array,
  },

  methods: {
    emitNewTask: function () {
      if (this.title.trim() == "" || this.description.trim() == "") return;
      this.$emit("newTask", {
        id: this.id,
        title: this.title.trim(),
        description: this.description.trim(),
        status: 0,
        project: this.selectedProject,
      });
      this.title = "";
      this.description = "";
      this.selectedProject = "";
    },
  },
};
</script>

<style >
.my-form {
  display: flex;
  flex-direction: column;
}

textarea {
  resize: vertical;
  max-height: 7rem;
}

.form-button {
  box-shadow: -2px -2px 6px rgba(101, 101, 101, 0.25),
    2px 2px 6px rgba(0, 0, 0, 0.25);
  color: #13afe0;
  cursor: pointer;
}
</style>