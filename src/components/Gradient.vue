<template lang="pug">
  .gradient
    GradientColor(
      v-for="(todo, index) in todos" 
      :key="todo.name" 
      :colors="todo.colors" 
      :active="index <= currentIndex"
    )
</template>

<script>
import { mapState } from 'vuex'
import GradientColor from './GradientColor'

export default {
  name: 'Gradient',
  components: {
    GradientColor
  },
  computed: {
    ...mapState(['todos', 'currentIndex'])
  }
}
</script>

<style lang="scss">
.gradient {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: -1;
}
</style>