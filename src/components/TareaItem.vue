<template>
    <div class="todo-item">

        <!-- v-bind asocia un elemento (clase, atributo, etc) a una variable de data() -->
        <h3 v-bind:class="{'is-complete':this.completed}">
            {{ tarea.title }}
        </h3>
        <div>
            <!-- 
                v-on:<nombre-evento> se usa para escuchar eventos y en caso de uno, 
                se llama al método asignado 
            -->
            <input type="checkbox" v-bind:checked="this.completed" v-on:change="marcarTarea"/>
            <button class="del" v-on:click="$emit('eliminar-tarea', tarea.id)" >X</button>
            <!-- Otra manera de emitir el evento -->
            <!-- <button class="del" @click="$emit('eliminar-tarea', tarea.id)" >X</button> -->
        </div>
        
    </div>
</template>
<script>
export default {
    name: "TareaItem",
    props: ["tarea"], //props que recibe un componente se definen en una lista de strings
    data() {
        return {
            completed: false
        }
    },
    created() {
        this.completed = this.tarea.completed
    },
    methods: {
        marcarTarea() {
            this.completed = !this.completed
        }
    }
}
</script>

<style scoped>
  .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;

    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 20em;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
    margin-left: 1em;
  }
</style>