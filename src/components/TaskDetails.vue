<template>
  <div class="task">
    <h3>{{ task.title }}</h3>
    <div class="icons">
      <i 
        class="material-icons" 
        @click="deleteTask">
        delete
      </i>
      <i 
        class="material-icons"
        :class="favoriteClass"
        @click="toggleFavorite">
        favorite
      </i>
    </div>
  </div>
</template>

<script>
import { useTaskStore } from '../stores/TaskStore'

export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    const taskStore = useTaskStore()

    const deleteTask = () => {
      taskStore.deleteTask(props.task.id)
    }

    const toggleFavorite = () => {
      taskStore.toggleFav(props.task.id)
    }

    const favoriteClass = computed(() => ({
      active: props.task.isFav,
    }))

    return { deleteTask, toggleFavorite, favoriteClass }
  },
}
</script>
