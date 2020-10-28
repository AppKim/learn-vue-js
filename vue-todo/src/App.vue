<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:childAddTodo="addTodo"></TodoInput>
    <TodoList
      v-bind:propsdata="todoItems"
      v-on:childRemoveTodo="removeTodo"
      v-on:childToggleComplete="toggleComplete"
    ></TodoList>
    <TodoFooter v-on:childClearAllTodo="clearAllTodo"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoInput from "./components/TodoInput";
import TodoList from "./components/TodoList";
import TodoFooter from "./components/TodoFooter";

export default {
  data: function() {
    return {
      todoItems: [],
    };
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  methods: {
    addTodo: function(todoItem) {
      var obj = { completed: false, item: todoItem };
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeTodo: function(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleComplete: function(todoItem) {
      // localstorage data update
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllTodo: function() {
      localStorage.clear();
      this.todoItems.splice(0);
    }
  },
  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter,
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}

input {
  border-style: groove;
}

button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
