<template>
  <div id="app">
    <section>
      <h1>TASK</h1>
      <Form :id="id" :projects="projects" @newTask="addTask($event)" />
      <Projects
        :projects="projects"
        @newProject="addProject($event)"
        @newFilter="changeFilter($event)"
      />
    </section>
    <section class="tasks">
      <Task
        v-for="task in filteredTasks"
        :key="task.id"
        :id="task.id"
        :title="task.title"
        :description="task.description"
        :status="task.status"
        :project="task.project"
        @incrementStatus="incrementTask($event)"
        @decrementStatus="decrementTask($event)"
        @deleteSelf="deleteTask($event)"
      />
    </section>
  </div>
</template>

<script>
import Form from "./components/Form";
import Task from "./components/Task";
import Projects from "./components/Projects.vue";

// TODO : clean form fields

export default {
  name: "App",
  components: {
    Form,
    Task,
    Projects,
  },

  data() {
    return {
      id: 0,
      tasks: [],
      selectedProject: "",
      filterBy: "",
      projects: ["Household", "Home work"],
    };
  },

  methods: {
    addTask: function ($event) {
      this.tasks.push({
        id: $event.id,
        title: $event.title,
        description: $event.description,
        status: $event.status,
        project: $event.project,
      });
      this.id += 1;
    },

    addProject: function ($event) {
      this.projects.push($event.newProject);
    },

    changeFilter: function ($event) {
      this.filterBy = $event.selectedFilter;
    },

    incrementTask: function ($event) {
      this.tasks.forEach((task) => {
        if (task.id == $event.id) task.status += 10;
      });
    },

    decrementTask: function ($event) {
      this.tasks.forEach((task) => {
        if (task.id == $event.id) task.status -= 10;
      });
    },

    deleteTask: function ($event) {
      this.tasks = this.tasks.filter((task) => task.id != $event.id);
    },
  },

  computed: {
    filteredTasks: function () {
      return this.filterBy == ""
        ? this.tasks
        : this.tasks.filter((task) => task.project == this.filterBy);
    },
  },
};
</script>

<style>
#app {
  display: grid;
  grid-template-columns: auto 1fr;
}

h1 {
  color: #ffffff;
  padding: 0.5rem;
  margin: 1rem;
  font-weight: bolder;
  font-size: 2rem;
}

.tasks {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}

input,
textarea,
button,
select {
  outline: none;
  font-size: 1.5rem;
  background-color: transparent;
  padding: 0.5rem;
  color: #d3d3d3;
  margin: 1rem;
  border: none;
  box-shadow: inset -4px -4px 8px rgba(82, 82, 82, 0.25),
    inset 4px 4px 8px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
}

.btn-danger {
  color: #e23221;
}

@media (max-width: 1200px) {
  .tasks {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 900px) {
  .tasks {
    display: grid;
    grid-template-columns: 1fr;
  }
}

@media (max-width: 700px) {
  .container {
    grid-template-columns: 1fr;
  }
}
</style>
