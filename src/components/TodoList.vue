<template lang="pug">
.todo-list(:class="{ 'todo-list__selected': selected }")
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
  height: 250px;
  transition: all .5s ease;

  ul {
    overflow-x: scroll;
    padding: 0px 0px 20px 10px;
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

  .todo {
    border-radius: 8px;
    background-color: white;
  }
}


  
.todo-list__selected {
  transform: scaleX(1.25);
}
</style>