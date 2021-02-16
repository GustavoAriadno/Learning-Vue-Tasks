<template>
  <div class="card-task">
    <h2>{{ title }}</h2>
    <p>{{ description }}</p>
    
    <div class="status">
      <span v-bind:style="statusStyle"></span>
    </div>

    <div class="task-actions">
      <button class="btn-sm" @click="increment">
        <span class="material-icons">add</span>
      </button>
      <button class="btn-sm" @click="decrement">
        <span class="material-icons">remove</span>
      </button>
      <!-- deleteTask -->
      <button class="btn-sm btn-danger">
        <span class="material-icons">delete</span>
      </button>

    </div>

    <!-- <div>task.project</div> -->
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    title: String,
    description: String,
    status: Number
  },

  computed: {
    statusStyle() {
      return 'width: ' + this.status + '%;';
    }
  },

  methods: {
    increment: function() {
      if (this.status < 100) {
        this.$emit("incrementStatus", {
          id: this.id
        });
      }
    },
    
    decrement: function() {
      if (this.status > 0) {
        this.$emit("decrementStatus", {
          id: this.id
        });
      }
    }
  }
};
</script>

<style>
.card-task{
	padding: 0px 15px 10px;
	box-shadow: -2px -2px 6px rgba(101, 101, 101, 0.25),
                2px 2px 6px rgba(0, 0, 0, 0.25);
	border-radius: 10px;
	margin: 1rem;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.status{
	height: 5px;
  margin: 2% 0%;
	background-color: #373737;
	border-radius: 10px;
}

.status span{
	height: 100%;
	background-color: #44D420;
	display: block;
	box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25),
              0px 0px 10px #44D420;
	border-radius: 10px;
}

.btn-sm {
	width: 36px;
	height: 36px;
	box-shadow: -2px -2px 6px rgba(91, 91, 91, 0.25),
                2px 2px 6px rgba(0, 0, 0, 0.25);
	border-radius: 18px;
	display: flex;
	align-items: center;
	justify-content: center;
	align-self: flex-end;
}

.task-actions{
	display: flex;
}
</style>