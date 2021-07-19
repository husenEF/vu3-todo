<template>
  <div class="container py-5 border my-5 rounded">
    <div class="row">
      <div class="col-12 text-center">
        <h3>Todo List</h3>
      </div>
    </div>
    <FormTodo @simpan="saveTodo" />
    <Todos :todos="todos.list" @done="doneTodo" @remove="deleteTodo" />
  </div>
</template>

<script >
import { reactive } from "@vue/reactivity";
import FormTodo from "./components/Form.vue";
import Todos from "./components/Todos.vue";
import { onMounted } from "@vue/runtime-core";
import { v4 as uuid4 } from "uuid";
export default {
  components: {
    FormTodo,
    Todos,
  },
  setup() {
    const todos = reactive({ list: [] });
    onMounted(() => {
      todos.list.push({ title: "todo 1", status: false, id: uuid4() });
    });
    const doneTodo = (id) => {
      console.log("donetodo", { id });
      const list = todos.list.map((e) => {
        if (e.id === id) {
          e.status = true;
        }
        return e;
      });
      console.log({ list: list });
      todos.list = list;
    };
    const saveTodo = (todo) => {
      // console.log("save todo", { todo });
      const list = todos.list;
      list.push({ title: todo, status: false, id: uuid4() });
    };

    const deleteTodo = (id) => {
      console.log("id", id);
      const list = todos.list.filter((e) => e.id !== id);
      todos.list = list;
    };

    // console.log({ uuid: uuid4() });
    return { todos, doneTodo, saveTodo, deleteTodo };
  },
};
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>


