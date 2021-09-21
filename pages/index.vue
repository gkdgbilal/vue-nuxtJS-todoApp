<template>
  <div>
    <div
      class="
        h-100
        w-full
        flex
        items-center
        justify-center
        bg-teal-lightest
        font-sans
      "
    >
      <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
        <div class="mb-4">
          <h1 class="text-grey-darkest">Todo List</h1>
          <!-- {{ todoList }} -->
          <div class="flex mt-4">
            <input
              v-model="title"
              class="
                shadow
                appearance-none
                border
                rounded
                w-full
                py-2
                px-3
                mr-4
                text-grey-darker
              "
              placeholder="Add Todo"
            />
            <button
              @click="addTodo"
              class="flex-no-shrink p-2 border-2 rounded text-teal border-teal"
            >
              Add
            </button>
          </div>
        </div>
        <div>
          <div
            class="flex mb-4 items-center"
            v-for="item in todoList"
            :key="item.id"
          >
            <p class="w-full text-grey-darkest">
              {{ item.title }}
            </p>
            <button
              @click="removeTodo(item.id)"
              class="
                flex-no-shrink
                p-2
                ml-2
                border-2
                rounded
                text-red
                border-red
              "
            >
              Remove
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    todoList() {
      return this.$store.getters["todo/todoList"];
    },
  },
  data() {
    return {
      title: "Todo Giriniz",
    };
  },
  methods: {
    addTodo() {
      let tempData = {
        id: this.todoList.length + 1,
        title: this.title,
      };
      return this.$store.dispatch("todo/addTodo", tempData);
    },
    removeTodo(id) {
      let tempData = {
        id: this.todoList.length + 1,
        title: this.title,
      };
      return this.$store.dispatch("todo/removeTodo", id);
    },
  },
  created() {
    this.$store.dispatch("todo/getTodoList");
  },
};
</script>
