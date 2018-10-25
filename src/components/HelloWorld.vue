<template>
<div class="wrapp">
  <ul>
    <li v-for="(item,index) in todoList" :key="index">
      <label :class="{done:item.isChecked}">
        <input  type="checkbox" v-model="item.isChecked">{{ item.title}}
      </label>
    </li>
  </ul>
  <p><input type="text" placeholder="todo" class="form" v-model="newItemTitle" @keyup.enter="addTodo(newItemTitle)"></p>
  <button class="todopush" @click="deleteTodo()">チェック済みのTODO削除</button>

  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      todoList: [],
      newItemTitle: ""
    };
  },
  methods: {
    addTodo: function(newItemTitle) {
      this.todoList.push({
        title: newItemTitle,
        isChecked: false
      });
      this.newItemTitle = "";
      this.saveTodo();
      this.loadTodo();
      console.log("push");
    },
    deleteTodo: function() {
      this.todoList = this.todoList.filter(function(item) {
        return item.isChecked === false;
      });
      this.saveTodo();
      this.loadTodo();
    },
    saveTodo: function() {
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    loadTodo: function() {
      this.todoList = JSON.parse(localStorage.getItem("todoList"));
      if (!this.todoList) {
        this.todoList = [];
      }
    }
  },
  mounted: function() {
    this.loadTodo();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapp {
  width: 320px;
  margin: 0 auto;
}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-direction: column;
}
li {
  display: inline-block;
  margin: 0 10px;
  text-align: left;
}
label {
  cursor: pointer;
}
a {
  color: #42b983;
}
.done {
  text-decoration: line-through;
}
.form,
.todopush {
  width: 160px;
  appearance: none;
  box-sizing: border-box;
  border-radius: 3px;
}
</style>
