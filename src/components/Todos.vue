<template>
  <div
    class="transition-all duration-500 w-full h-screen mx-auto py-16 px-4 lg:px-56 relative group bg-white flex flex-col items-center justify-center"
  >
    <div
      class="topContainer w-full h-screen mx-auto py-12 px-4 relative group bg-white flex flex-col items-center justify-center"
    >
      <h1 class="font-bold text-7xl text-[#8d60c7]">Todo App</h1>
      <div class="input my-10 w-full px-10 flex flex-wrap gap-4">
        <input
          class="w-full py-3 px-8 outline-none border-none placeholder-gray-600 rounded-md text-black bg-[#c791d46e]"
          type="text"
          placeholder="To do "
          v-model="newTodo"
        />
        <button
          class="w-200 cursor-pointer bg-[#8d60c7] text-white font-bold py-3 px-8 rounded-md"
          @click="addTodo()"
        >
          Add
        </button>
      </div>
    </div>
    <ul class="w-full px-14">
      <li
        class="bg-[#c791d46e] rounded-2xl w-full py-4 pl-6 pr-9 my-4 font-bold text-xl relative"
        v-for="(todo, index) in Todos"
        :key="index"
      >
        {{ todo }}
        <div class="absolute right-3 top-2 mt-2 px-3">
          <box-icon
            type="solid"
            class="cursor-pointer mr-3"
            @click="removeTodo(index)"
            name="check-circle"
            color="#8d60c7"
            size="36px"
          ></box-icon>
          <box-icon
            name="trash"
            color="black"
            class="cursor-pointer"
            @click="removeTodo(index)"
            size="36px"
          ></box-icon>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import "boxicons";

export default {
  name: "TodoList",
  data() {
    return {
      newTodo: "",
      Todos: ["First Todo "],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo == "") {
        this.newTodo = "Nothing to do ";
      } else {
        this.Todos.push(this.newTodo);
        localStorage.setItem("Todos", JSON.stringify(this.Todos));
        this.newTodo = "";
      }
    },
    removeTodo(index) {
      this.Todos.splice(index, 1);
      localStorage.setItem("Todos", JSON.stringify(this.Todos));
    },
  },
  created: function () {
    this.Todos = JSON.parse(localStorage.getItem("Todos"));
    this.Todos = this.Todos || [];
  },
};
</script>
