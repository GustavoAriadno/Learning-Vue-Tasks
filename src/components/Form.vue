<template>
  <div>
    <form class="my-form" v-on:submit.prevent>
      <input class="my-input" type="text" placeholder="Title" v-model="title"/>
      <textarea class="my-textarea" placeholder="Description" v-model="description"/>
        
      <button class="my-button" @click="emitNewTask">Salvar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
    };
  },

  props: {
    id: Number
  },

  methods: {
     emitNewTask: function() {
      this.$emit("newTask", {
        id: this.id,
        title: this.title,
        description: this.description,
        status: 0
      });
    }
  }
};
</script>

<style>
.my-form {
	display: flex;
	flex-direction: column;
}

.my-input, .my-textarea, .my-button, .my-select {
	outline: none;
	font-size: 1.5rem;
	background-color: transparent;
	padding: .5rem;
	color: #d3d3d3;
	margin: 1rem;
	border: none;
	box-shadow: inset -4px -4px 8px rgba(82, 82, 82, 0.25),
              inset 4px 4px 8px rgba(0, 0, 0, 0.25);
	border-radius: 10px;
}

.my-textarea {
  resize: vertical;
  max-height: 7rem;
}

.my-button {
	box-shadow: -2px -2px 6px rgba(101, 101, 101, 0.25),
                2px 2px 6px rgba(0, 0, 0, 0.25);
	color: #13afe0;
	cursor: pointer;
}
</style>