<template>
  <div class="row">
    <div class="col-12">
      <div class="card">
        <div class="card-body">
          <form @submit.prevent="save()" class="row">
            <div class="col-md-9 col-sm-8">
              <input
                type="text"
                class="form-control"
                id="todo"
                placeholder="Todo"
                v-model="todo"
                required
              />
            </div>
            <div class="col-md-3 col-sm-4">
              <button type="submit" class="btn btn-primary mb-3 w-100">
                Tambah Todo
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  setup(props, { emit }) {
    const todo = ref("");

    const save = () => {
      emit("simpan", todo.value);
      todo.value = "";
    };

    return { todo, save };
  },
};
</script>