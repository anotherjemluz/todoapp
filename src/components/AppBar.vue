<template lang="pug">
  div.app-bar
    span.app-bar_l(@click="$emit('left')")
      i(:class="['fa', `fa-${left}`]")
    h1 {{ title }}
    span.app-bar_r(@click="$emit('right')")
      i(:class="['fa', `fa-${right}`]")

</template>

<script>
export default {
  name: 'AppBar',
  props: {
    title: {
      type: String,
      default: ''
    },
    left: {
      type: String,
      default: 'chevron-left'
    },
    right: {
      type: String,
      default: 'ellipsis-v'
    }
  }
}
</script>

<style lang="scss">
.app-bar {
  z-index: 1;

  display: flex;
  align-items: center;

  height: 44px;
  font-size: 15px;

  h1 {
    display: flex;
    justify-content: center;
    flex: 1;
  }

  span {
    padding: 0 20px;
  }
}
</style>