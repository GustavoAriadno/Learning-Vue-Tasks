<template>
  <div id="app">
    <section>
      <h1>TASK</h1>
        <!-- projects= -->
      <Form :id="id" @newTask="addTask($event)"/>
      <!-- <Projects
        projects=
        addProject
        filter -->
    </section>
    <section class="taks">
        <div  v-for="task in tasks" :key="task.id">
        <Task
          :id="task.id"
          :title="task.title"
          :description="task.description"
          :status="task.status"
          @incrementStatus="incrementTask($event)"
          @decrementStatus="decrementTask($event)"/>
      </div>
    </section>
  </div>
</template>

<script>
import Form from "./components/Form"
import Task from "./components/Task"

export default {
  name: "App",
  components: {
    Form,
    Task
  },

  data() {
    return {
      id: 0,
      tasks: [],
      projects: []
    };
  },

  methods: {
    addTask: function($event) {
      this.tasks.push({
        id: $event.id,
        title: $event.title,
        description: $event.description,
        status: $event.status
      });
      this.id += 1;
    },

    incrementTask: function($event) {
      this.tasks.forEach(task => {
        if(task.id == $event.id) {
          task.status += 10;
        }
      });
    },

    decrementTask: function($event) {
      this.tasks.forEach(task => {
        if(task.id == $event.id) {
          task.status -= 10;
        }
      });
    },
  }
};
</script>

<style>
#app {
	display: grid;
	grid-template-columns: auto 1fr;
  background-color: #1f1f1f;
}

h1 {
	color: #ffffff;
  padding: .5rem;
  margin: 1rem;
	font-weight: bolder;
	font-size: 2rem;
}

.taks {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
}

.btn-danger {
	color: #e23221;
}

@media (max-width: 1200px) {
	.taks {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	}
}

@media (max-width: 900px) {
	.taks {
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
