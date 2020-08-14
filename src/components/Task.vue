<template lang="pug">
  transition(name="fade")
    .task(v-if="!task.deleted")
      input(:id="id" type="checkbox" v-model="task.done")
      label(:for="id") {{ task.title }}

      transition(name="fade")
        span.task_delete(v-show="task.done" @click="deleteTask")
          i.fa.fa-trash

</template>

<script>
export default {
  name: 'Task'
}
</script>

<style lang="scss">

</style>