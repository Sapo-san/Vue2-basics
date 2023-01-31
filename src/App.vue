<template>
  <!-- Dentro de template solo puede haber un elemento (y dentro de ese elemento pueden haber varios más) -->
  <!-- En este caso el unico elemento es el div con id=app -->
  <div id="app">
    <div class="main-text">
      <h1>Repaso Vue2</h1>
      <h3> Aplicación para Tareas / Recordatorios </h3>
      <p>Ver código de fuente para comentarios sobre el funcionamiento de Vue2</p>
    </div>

    <!-- v-on escucha el evento "add-tarea" y de recibirlo, llama al metodo addTarea() -->
    <AddTarea v-on:add-tarea="addTarea"/>

    <!-- Acá v-bind asocia el prop "tareas" del componente con el "data() -> tareas" del estado -->
    <ListaTareas v-bind:tareas="tareas" v-on:eliminar-tarea="eliminarTarea"/>
  </div>
</template>

<script>
/* En la sección Script va el javascript asociado al template */

// imports de otros componentes
import AddTarea from './components/AddTarea.vue'
import ListaTareas from './components/ListaTareas.vue'

// Información del componente
export default {
  name: 'App', // Nombre del componente
  components: {
    ListaTareas,
    AddTarea
},
  data() { // Este método guarda la información del componente (similar al estado en React)
    return {
      tareas: [
      {
          id: 0,
          title: "Tarea 1",
          completed: true
        },
        {
          id: 1,
          title: "Tarea 2",
          completed: false
        },
        {
          id: 2,
          title: "Tarea 3",
          completed: false
        },
      ],
      contador: 3
    }
  },
  // En "methods" se definen los métodos del componente. Esto no incluye los
  // métodos del Ciclo de Vida (created, beforeCreate, etc...)
  methods: { 
    eliminarTarea(id) {
      console.log("Eliminando tarea con ID:", id)
      this.tareas = this.tareas.filter((tarea) => {
        if (tarea.id == id) return false;
        return true
      })
    },
    addTarea(tarea) {
      tarea.id = this.contador
      this.contador++
      this.tareas.push(tarea)
    }
  }
}
</script>

<style>
/* 
  Estilos del componente
  Para hacer que apliquen solo a este componente y no
  a toda la hoja de CSS, se utiliza <style scoped>
  */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
    background-color: rgb(165, 255, 225);
    
    text-align: center;
    width: 100%;
    
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .main-text {
    margin: 2em;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
