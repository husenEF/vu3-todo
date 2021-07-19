<template>
  <ul class="my-5 list-group">
    <li v-for="(todo, i) in todos" :key="i" class="list-group-item">
      <span :class="{ finish: todo.status }">{{ todo.title }}</span>
      <div class="btn-group float-end" role="group" aria-label="Basic example">
        <button class="btn btn-success btn-sm" @click="done(todo.id)">
          Finish
        </button>
        <button class="btn btn-primary btn-sm" @click="deleted(todo.id)">
          Delete
        </button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },
  
  setup({ todos }, { emit }) {
    const done = (i) => {
      emit("done", i);
    };
    const deleted = (i) => {
      emit("remove", i);
    };
    console.log({ todos });
    return { done, deleted };
  },
};
</script>

<style scoped>
.finish {
  color: red;
  text-decoration: line-through;
}
</style>