<template>
  <div class="app" :class="mode">
      <TodoForm :mode="mode" class="todoform"/>
        <div class="todoform2">
            <div class="seccionn">
                <TodoTable         
                    v-for="tarea in tareas" :key="tarea.id"
                    :tarea="tarea"
                    
                    />
            </div>
            <div class="seccion2">
                <TodoFilter/>
            </div>
        </div>

  </div>
</template>

<script>
import { provide, ref, watchEffect } from 'vue'
import TodoForm from './TodoForm.vue'
import TodoTable from './TodoTable.vue'
import TodoFilter from './TodoFilter.vue'
export default {
    components:{
        TodoForm,
        TodoTable,
        TodoFilter
    },
    setup(){
        const mode = ref('dark')
        const tareas = ref([])
        const savetareas = ref([])
        const filtro = ref('-')


        provide('tareas', tareas)
        provide('savetareas', savetareas)
        provide('mode', mode)
        provide('filtro', filtro)

        if(localStorage.getItem('tareas')){
            tareas.value = JSON.parse(localStorage.getItem('tareas'))
        }
        watchEffect(()=>{
            localStorage.setItem('tareas', JSON.stringify(tareas.value))

        })
        return {mode, tareas, filtro}
    }
}
</script>

<style>
* {
    font-family: 'Josefin Sans', sans-serif;
    padding: 0;
    margin: 0;
    font-size: 18px;
}
@media (max-width: 4000px){
    .todoform2{
        display: block;
        height: 100%;
        width: 38vw;
        padding: 0rem 30vw;
    }
}
@media (max-width: 1200px){
    .todoform2{
        display: block;
        height: 100%;
        width: 80vw;
        padding: 0.5rem 10vw;
        /* margin: 100px; */
    } 
}
.seccionn{
  box-shadow: 1px 1px 30px rgb(207, 203, 203);
  border-radius: 2px;
}

.dark .seccionn{
  box-shadow: 1px 1px 30px rgb(27, 25, 25);
  border-radius: 5px;
}
@media (max-width: 4000px){
    .app{
        position:absolute;
        width: 100vw;
        background-image: url('../images/bg-desktop-light.jpg');
        background-size: contain;
        background-repeat: no-repeat;
        background-position: top;
        box-sizing: content-box;
        min-height: 100vh;
        color:hsl(235, 19%, 35%);
    }
    .dark{
        position:absolute;
        width: 100vw;
        background-image: url('../images/bg-desktop-dark.jpg');
        background-size: contain;
        background-repeat: no-repeat;
        background-position: top;
        box-sizing: content-box;
        min-height: 100vh;
        color: hsl(234, 39%, 85%);
        background-color: hsl(235, 21%, 11%);
    }
}

@media (max-width: 700px){
    .app{
        position:absolute;
        width: 100vw;
        background-image: url('../images/bg-mobile-light.jpg');
        background-size: contain;
        background-repeat: no-repeat;
        background-position: top;
        box-sizing: content-box;
        min-height: 100vh;
        color:hsl(235, 19%, 35%);
    }
    .dark{

        background-image: url('../images/bg-mobile-dark.jpg');
        background-size: contain;
        background-repeat: no-repeat;
        background-position: top;
        box-sizing: content-box;
        min-height: 100vh;
        color: hsl(234, 39%, 85%);
        background-color: hsl(235, 21%, 11%);
    }
}
</style>