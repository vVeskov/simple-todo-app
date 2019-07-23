<template>
  <p>
    <label for="new-task" Add Item></label>
    <input id="new-task" type="text" v-model="newToDoName"/>
    <button @click="addNewToDo">Add</button>
  </p>
</template>

<script>
export default {
  name: "add-todo",
  data() {
    return {
      newToDoName: ""
    };
  },
  methods: {
    addNewToDo() {
      if (this.newToDoName.trim().length < 1) {
        return
      }
      this.$emit('add-todo',this.newToDoName);
      this.newToDoName = "";
    }
  }
};
</script>

<style scoped>
label[for="new-task"] {
  display: block;
  margin: 0 0 20px;
}
input#new-task {
  float: left;
  width: 318px;
}
p > button:hover {
  color: #0fc57c;
}
</style>
