<template>
  <div id="app">
    <md-card>
      <md-card-header>
        <div class="md-title">Todo App</div>
        <div class="md-subhead">by Carlos Scarpantonio</div>
      </md-card-header>
    </md-card>

    <md-field>
      <md-input
        class="input-todo"
        v-model="newTodo"
        @keydown.enter="addTodo()"
        placeholder="Add a todo"
      ></md-input>
    </md-field>

    <div>
      <!-- m-list actua como ul & m-list-item actua como li -->
      <md-list v-for="todo in todos" :key="todo.id">
        <md-list-item class="todo-item-label" @dblclick="edited = !edited">
          <span class="check-postiion">
            <input
              class="check"
              type="checkbox"
              id="checkbox"
              v-model="checked"
              @click="checkedBtn(todo)"
            />
          </span>

          <!-- <md-field>
            <span class="md-list-item-text">
              <md-input
                v-bind:class="{ edited: edited }"
                @keydown.enter="edited = !edited"
                type="text"
                v-model="todo.label"
                placeholder="edit todo here"
              />{{ todo.label }}</span
            >
          </md-field> -->

          <span class="md-list-item-text"
            ><input
              v-bind:class="{ edited: edited }"
              @keydown.enter="edited = !edited"
              type="text"
              v-model="todo.label"
              placeholder="edit todo here"
            />
            {{ todo.label }}</span
          >

          <md-button class="md-accent" @click="removeTodo(todo)"
            ><md-icon>highlight_off</md-icon></md-button
          >
        </md-list-item>
      </md-list>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // this array are our todo items
      todos: [],
      newTodo: "",
      edited: true
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.newTodo,
        completed: false
      });
      this.newTodo = "";
    },
    removeTodo(todo) {
      // aqui el index para saber donde esta ubicado el item que seleccionamos. el numero de index. para luego aplicar splice para q lo elimine. cuando le damos click aqui arriba agarra el todo y lo mete dentro de la funcion.
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    checkedBtn(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      alert(todo);
      // todo.edited = true;
      // this.todos.edited = true;
    }
  }
};
</script>

<style>
#app {
  margin: 100px;
  text-align: center;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

li {
  list-style-type: none;
}

.input-todo {
  text-align: center;
  /* border: solid 2px;
  border-radius: 10px;
  height: 40px;
  width: 250px; */
}

.edited {
  display: none;
}

.check {
  margin-right: 10px;
}

/* check postion/desing */
.check-postiion {
  margin-right: 30px;
}

.deleteBtn {
  margin-left: 10px;
}
</style>

// Ver el video acerca de la lista de todo para poner la funcion de que no se
pueda agregar info si el input esta vacio, .
