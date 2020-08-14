<template lang="pug">
  .todo(:class="{ todo__selected: selected }")
    .todo_head(@click="handleClick")
      .todo_icon(:style="{ color }")
        i(:class="['fa', `fa-${todo.icon}`]")
      
      .todo_menu 
        i.fa.fa-ellipsis-v

    .todo_body
      p.todo_tips {{ todo.tasks.length }} Tarefas
      h3.todo_title {{ todo.name }}
      
      .todo_progress
        span.todo_progress_line
          i(:style="{ width: progress, backgroundImage: progressColor }")
        
        span.todo_progress_num {{ progress }}

      .todo_tasks
        h4.todo_subtitle(v-if="todayTasks.length") Hoje
        ul
          li(v-for="task in todayTasks" :key="task.id")
            Task(:task="task")

        h4.todo_subtitle(v-if="tomorrowTasks.length") Amanhã
        ul
          li(v-for="task in tomorrowTasks" :key="task.id")
            Task(:task="task")

        h4.todo_subtitle(v-if="outdatedTasks.length") Desatualizado
        ul
          li(v-for="task in outdatedTasks" :key="task.id")
            Task(:task="task")
</template>

<script>
import { today, tomorrow } from '../shared'
import Task from './Task.vue'

export default {
  name: 'Todo',
  components: {
    Task
  },
  props: {
    todo: {
      type: Object,
      required: true
    },
    selected: {
      type: Boolean
    }
  },
  computed: {
    color () {
      return this.todo.colors[0]
    },
    progress () {
      const totalCount = this.todo.tasks.filter(t => !t.deleted).length
      const doneCount = this.todo.tasks.filter(t => !t.deleted && t.done).length
      return `${Math.round((doneCount / totalCount) * 100)}%`
    },
    progressColor () {
      const colorBottom = `${this.todo.colors[0]}`
      const colorTop = `${this.todo.colors[1]}`
      return `linear-gradient(to bottom, ${colorBottom}, ${colorTop})`
    },
    todayTasks () {
      return this.todo.tasks.filter(task => {
        return task.date >= today && task.date < tomorrow
      })
    },
    tomorrowTasks () {
      return this.todo.tasks.filter(task => {
        return task.date >= tomorrow
      })
    },
    outdatedTasks () {
      return this.todo.tasks.filter(task => {
        return task.date < today
      })
    }
  },
  methods: {
    handleClick() {
      const appRect = document.querySelector('#app').getBoundingClientRect();
      const elRect = this.$el.getBoundingClientRect();
      const todo = this.todo;
      const rect = {}

      rect.top = elRect.top - appRect.top
      rect.left = elRect.left - appRect.left

      rect.width = elRect.width
      rect.height = elRect.height

      rect.appWidth = appRect.width
      rect.appHeight = appRect.height

      this.$emit('select', { rect, todo });
    }
  }
}
</script>

<style lang="scss">
.todo {
  flex: 1;
  width: 70vw;
  margin: 0 8px;
  overflow: hidden;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.2);
  color: #666;

  border-radius: 8px;
  background-color: white;
}
.todo__selected {
  visibility: hidden;
}
.todo_head {
  display: flex;
  padding: 20px;
  height: 44px;
  justify-content: space-between;
  align-items: flex-start;
  transform: translate3d(0, 0, 0);
  will-change: transform;
}
.todo_body {
  // display: flex;
  width: 80vw;
  padding: 20px;
  // transform: translate3d(0, 189px, 0);
  will-change: transform;
}
.todo_icon {
  display: flex;
  width: 44px;
  height: 44px;
  border: 1px solid #decfcf;
  border-radius: 100%;
  justify-content: center;
  align-items: center;
  font-size: 18px;
}
.todo_menu {
  color: #decfcf;
}
.todo_tips {
  opacity: 0.6;
  font-size: 13px;
  font-weight: 600;
}
.todo_title {
  margin-top: 6px;
  font-size: 32px;
}
.todo_progress {
  display: flex;
  align-items: center;
  margin-top: 30px;
}
.todo_progress_line {
  margin-right: 10px;
  flex: 1;
  height: 3px;
  background-color: #eee;

  i {
    display: block;
    height: 100%;
    transition: all .3s ease;
  }

  .todo_progress_num {
    font-size: 12px;
  }

  .todo_tasks {
    opacity: 0;
    transform: scale3d(1, 0, 1);
  }

  .todo_subtitle {
    margin-top: 32px;
    margin-bottom: 8px;
    color: #999;
  }
}
</style>