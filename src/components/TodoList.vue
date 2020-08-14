<template lang="pug">
.todo_list(:class="{ 'todo-list__selected': selected }")
  ul(:style="{ width: `${todos.length * 100}` }")
    li(
      v-for="todo in todos"
      :key="todo.name"
      :style="{ transform: `translate3d(-${currentIndex * 100}%, 0, 0)` }"
    )
      Todo(
        :todo="todo"
        :selected="selected && selected.todo === todo"
        @select="selectTodo"
      )
</template>

<script>
import { mapState, mapMutations } from 'vuex';
import Todo from "./Todo";

export default {
  name: "TodoList",
  components: {
    Todo,
  },
  computed: {
    ...mapState(['todos', 'currentIndex', 'selected'])
  },
  methods: {
    ...mapMutations(['selectTodo', 'nextTodo', 'prevTodo'])
  }
};
</script>

<style lang="scss">
.todo-list {
  padding: 0 32px;
  height: 400px;
  transition: all .5s ease;
}

ul {
  overflow-x: scroll;
  padding-left: 20px;
}

ul,
ul li {
  display: flex;
  height: 100%;
}

ul li {
  flex: 1;
  transition: transform .5s ease;  
}
  
.todo-list__selected {
  transform: scaleX(1.25);
}
</style>