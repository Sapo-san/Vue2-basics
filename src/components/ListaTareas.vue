<template>
    <div class="todo-list">
        <div v-for="tarea in tareas" v-bind:key="tarea.id">
            <TareaItem 
              v-bind:tarea="tarea"
              v-on:eliminar-tarea="$emit('eliminar-tarea', tarea.id )"
            />
        </div>
    </div>
</template>
<script>
import TareaItem from './TareaItem.vue';

export default {
    name: "ListaTareas",
    props: ["tareas"],
    components: { TareaItem }
}
</script>

<style scoped>
  .todo-list {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50em;
    flex-direction: column;
  }
</style>