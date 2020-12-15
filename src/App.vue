
<template>
  <div>
    <md-card>
      <md-card-header>
        <div class="md-title">
          <img class="logo" src="../public/img/logo.png" alt="logo" />
        </div>
      </md-card-header>
    </md-card>

    <md-field>
      <md-input
        type="text"
        class="todo-input"
        placeholder="Add a todo here"
        v-model="newTodo"
        @keyup.enter="addTodo"
      ></md-input>
    </md-field>

    <div v-for="(todo, index) in todosFiltered" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed" />
        <div
          v-if="!todo.editing"
          @dblclick="editTodo(todo)"
          class="todo-item-label"
          :class="{ completed : todo.completed }"
        >{{ todo.title }}</div>
        <input
          v-else
          class="todo-item-edit"
          type="text"
          v-model="todo.title"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)"
          v-focus
        />
      </div>
      <div class="remove-item" @click="removeTodo(index)">
        <md-icon>highlight_off</md-icon>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      newTodo: "",
      beforeEditCache: "",
      filter: "all",
      todos: [
        {
          id: 1,
          title: "To do Example",
          completed: false,
          editing: false
        }
      ]
    };
  },
  computed: {
    // filtered to do.
    todosFiltered() {
      if (this.filter == "all") {
        return this.todos;
      }
      return this.todos;
    }
  },
  // disable edit mode when clicked. Customer directives to fix focus issue.
  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
        editing: false
      });
      this.newTodo = "";
      this.idForTodo++;
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    // disable edit mode when clicked.
    doneEdit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style >
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@100;300;800&family=Raleway&display=swap");

.logo {
  width: 100%;
  max-width: 100px;
}

* {
  text-align: center;
  font-family: "Montserrat", sans-serif;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 100px;
  margin-right: 100px;
}
.remove-item {
  cursor: pointer;
  margin-left: auto;
  color: lightgreen;
}
.todo-item-left {
  display: flex;
  align-items: center;
}
.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  /* margin-left: 12px; */
}
.todo-item-edit {
  font-size: 16px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
