<script>
// give each todo a unique id
let id = 0;
const idOpt = "";

export default {
  // component options
  // declare some reactive state here.
  data() {
    return {
      message: "Hello World!",
      text: "",
      type: "",
      awesome: true,
      counter: {
        count: 0,
      },
      titleClass: "title",
      titleOption: "lista",
      newOption: "",
      options: [
        { idOpt: "A", text: "Learn HTML" },
        { idOpt: "B", text: "Learn JavaScript" },
        { idOpt: "C", text: "Learn Vue" },
        { idOpt: "", text: "Never" },
      ],
      newTodo: "",
      todos: [
        { id: id++, text: "Learn HTML" },
        { id: id++, text: "Learn JavaScript" },
        { id: id++, text: "Learn Vue" },
      ],
    };
  },
  methods: {
    increment() {
      // update component state
      this.counter.count++;
    },
    onInput(e) {
      // a v-on handler receives the native DOM event
      // as the argument.
      this.text = e.target.value;
    },
    toggle() {
      this.awesome = !this.awesome;
    },
    onRadio(e) {
      this.type = e.target.value;
    },
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo });
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
  },
};
</script>

<template>
  <h1 :class="titleClass">{{ message }}</h1>
  <h1>{{ message.split("").reverse().join("") }}</h1>
  <p>Aumentar: {{ counter.count }}</p>
  <button @click="increment">Incrementar</button>,<br />
  <input v-model="text" placeholder="Type here" />
  <p>{{ text }}</p>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
  <ul :class="titleOption">
    <li v-for="option in options" :key="option.idOpt">
      <input
        :class="TitleOption"
        v-model="type"
        type="radio"
        name="option"
        :value="option.idOpt"
      />
      {{ option.text }}
    </li>
  </ul>
  <div v-if="type === 'A'">Respuesta: A</div>
  <div v-else-if="type === 'B'">Respuesta: B</div>
  <div v-else-if="type === 'C'">Respuesta: C</div>
  <div v-else>Respuesta: Never</div>
  <div>Example toDoList with v-for directive</div>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" />
    <button>Add Todo</button>
  </form>
  <ul :class="titleOption">
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">
        <i class="fas fa-spinner"></i>
      </button>
    </li>
  </ul>
</template>

<style>
.title {
  color: red;
}
.lista {
  list-style: none;
}
</style>
