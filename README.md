# Vue2 Repaso / Cheatsheet
Repositorio donde aplico los conceptos básicos de Vue2.

Video de referencia que usé para crear este repositorio: [Vue2 Crash Course - Traversy Media](https://www.youtube.com/watch?v=qZXt1Aom3Cs)

### Para instalar dependencias
```
> npm install
```

### Para compilar para desarrollo (con hot-reload)
```
> npm run serve
```
Nota: correr comandos en carpeta raíz del proyecto.

# Apuntes Vue2
Aplicación tiene un `main.js` que carga componente `App.vue`

Estructura del proyecto:
```
.
├── node_modules
├── public
└── src/
    ├── main.js
    ├── App.vue
    ├── assets/
    │   └── ...
    └── components/
        └── ...
```
En carpeta `src/assets` se pueden dejar imágenes/etc para ocupar en el proyecto.

Archivo `main.js` carga `App.vue` y monta la aplicación

Todos los componentes tienen la siguiente estructura (incluido `App.vue`)
```vue
<template>
    <!-- HTML dinamico -->
</template>
<script>
    /* Javascript asociado al componente */

    ...

    // Export del componente
    export default {
        // Nombre del componente, Opcional
        name: "Nombre del componente", 

        // Props del componente, cada string es un prop. Opcional
        props: ["props", "del", "componente"], 
        
        // Estados del componente, Opcional
        data() { 
            return {
                estado1: "...",
                estado2: true,
                ...
            }
        }

        // Métodos asociados al componente, opcional
        methods: {
            metodo1() {
                ...
            },
            metodo2() {
                ...
            }
        },

        // Fuera de "methods" pueden ir otros metodos,
        // por ejemplo, los metodos del ciclo de vida
        // del componente (beforeCreate, created, etc...)
        ...
    }

</script>
<style>
    /* CSS (poner scoped despues del primer style para asocialrlo únicamente al componente) */
</style>
```
## Notación Vue en HTML dinámico
### v-bind
Para asociar un dato de estado a un elemento html se usa `v-bind`.

Ejemplo (asociar estado a nombre de clase)
```vue
<template>
    <h1 v-bin:class="claseDelDiv">Titulo</h1>
</template>
<script>
    export default {
        data() {
            return {
                claseDelDiv: "clase"
            }
        }
    }
</script>
```
Ejemplo (asociar estado a prop de componente)
```vue
<template>
    <Componente1 v-bind:nombre-prop="prop"/>
    <Componente2 v-bind:nombre-prop="this.prop"/>
</template>
<script>
    export default {
        data() {
            return {
                prop: "prop-a-mandar-a-ambos-componentes"
            }
        }
    }
</script>
```

### v-for
Para renderizar un array o iterable, se utiliza `v-for`:
```vue
<div v-for="elemento in lista">
    <p>{{elemento.atributo}}</p>
</div>
```
Recordar añadir una key a cada elemento con `v-bind`.
```vue
<div v-for="elemento in lista" v-bind:key="elemento.key">
    <p>{{elemento.atributo}}</p>
</div>
```

### v-show
Muestra o esconde HTML segun un booleano proveniente de `data()`
```vue
<template>
    <!-- <div v-show="this.booleano"> -->
    <div v-show="booleano">
        <h1>Texto que se esconde segun booleano</h1>
    </div>

</template>
<script>
    export default {
        data() {
            return {
                booleano: true
            }
        }
    }
</script>
```
### v-if
Muestra o esconde HTML segun un booleano proveniente de `data()` o una expresión que devuelva un booleano
```vue
    <div v-if="1 === 1 ? true : false">
        <h1>Texto que se esconde segun expresión</h1>
    </div>

```




