<template lang="pug">
  div.home
    AppBar(title="TODO" left="bars" right="search")
    Avatar
    Gradient
    TodoList

</template>

<script>
import AppBar from '../components/AppBar'
import Avatar from '../components/Avatar'
import Gradient from '../components/Gradient'
import TodoList from '../components/TodoList'

export default {
  name: 'Home',
  components: {
    AppBar,
    Avatar,
    Gradient,
    TodoList
  },
}
</script>

<style lang="scss">
.home {
  // background-color: #333;
  height: 100%;
  width: 100%;
  // overflow: hidden;
  overflow: scroll;
  color: white;
}
</style>