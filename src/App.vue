<template>
  <div id="app" class="container is-fluid text-center">
    <h1>Todo App</h1>
    <form @submit.prevent="formSubmitted()">
      <div style="display: inline-block;">
        <input
          type="text"
          class="input is-primary input-p"
          v-model="newTodo"
          placeholder="Go Paragliding ✈..."
        />
        <button class="button is-link margin-4" type="submit">Add Todo</button>
      </div>
    </form>
    <div class="todoList">
      <ul class="menu-list">
        <li class="margin-4" v-for="(todo, i) of this.todos" :key="todo.title">
          <h2 class="h2-thing">
            <span :class="{ isDone: todo.done }">{{ todo.title }}</span>
            <!-- eslint-disable-next-line -->
            <button v-if="!todo.done" class="button is-success don" @click="toggleDone(todo, i)">
              <svg
                viewBox="0 0 24 24"
                class="svgs"
                stroke="white"
                stroke-width="2"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                <polyline points="22 4 12 14.01 9 11.01" />
              </svg>
            </button>
            <!-- eslint-disable-next-line -->
            <button class="button is-danger don" @click="todoDelete(todo, i)">
              <svg
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="svgs"
              >
                <polyline points="3 6 5 6 21 6" />
                <path
                  d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"
                />
                <line x1="10" y1="11" x2="10" y2="17" />
                <line x1="14" y1="11" x2="14" y2="17" />
              </svg>
            </button>
          </h2>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => {
    return {
      newTodo: "",
      todos: []
    };
  },
  watch: {
    todos: {
      handler() {
        localStorage.todos = JSON.stringify(this.todos);
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.todos) {
      this.todos = JSON.parse(localStorage.todos);
    }
  },
  methods: {
    formSubmitted() {
      console.log("form has been submitted");
      console.log(this.newTodo);
      if (this.newTodo.trim() != "") {
        this.todos.push({
          title: this.newTodo.trim(),
          done: false
        });
      }
      this.newTodo = "";
    },
    toggleDone(todo) {
      todo.done = true;
    },
    todoDelete(todo, index) {
      // remove that ele from the array\
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style>
h1 {
  font-size: 3em;
}
h2 {
  font-size: 2em;
}
.input-p {
  margin-top: 1em;
}
.margin-4 {
  margin-top: 1.5rem;
}
.isDone {
  text-decoration: line-through;
}
span {
  margin-left: 1em;
}
.text-center {
  text-align: center;
}
.svgs {
  width: auto;
  height: 80%;
}
.don {
  margin-left: 5px;
}
.todolist ul li {
  display: flex;
}
</style>
