<template>
    <div>
        <!--
            Implementación de un formulario con preventDefault

            addTarea es el metodo que se llama cuando se evita que
            se refresque la página
        -->
        <form @submit.prevent="addTarea" class="añadir-tarea">
            <!--
                Para mapear un campo del formulario al estado, se usa v-model
                Recordar agregar un campo en data() con el mismo nombre

                en este caso es v-model=tarea
                data() -> tarea: "" (string vacio)
            -->
            <input type="text" v-model="tarea" name="tarea" placeholder="Escribe tarea aquí"/>
            <input type="submit" value="Añadir" class="btn"/>
        </form>
    </div>
</template>
<script>
export default {
    name: "AddTarea",
    data() {
        return {
            tarea: ""
        }
    },
    methods: {
        addTarea() {
            /*
                this.$emit hace que el componente emita un evento. la función emit recibe el nombre
                del evento (string) y el el objeto con la info del evento en el 2do parámetro

                en este caso, la info del evento es la info de la tarea creada
            */
            if (this.tarea !== "") {
                this.$emit('add-tarea', { 
                    title: this.tarea,
                    completed: false
                })
                this.tarea = ""
                this.$emit('esconder-add-tarea')
            }
            
        }
    }
}
</script>
<style>
    .añadir-tarea {
        margin-bottom: 1em;
    }

    .añadir-tarea input {
        border: none;
        padding: 0.5em;
        margin-right: 1em;
    }
</style>