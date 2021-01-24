<template>
  <div class="footer">
      <p class="footer__p">{{long}} items left</p>
      <div class="foooter__tareas">
        <button @click="all">All</button>
        <button @click="clearactive">Active</button>
        <button @click="clearcompelte">Completed</button>
      </div>
      <button @click="cleartareas">Clear Completed</button>
        
  </div>

</template>

<script>
import { computed, inject, ref } from 'vue'
export default {
    setup(){
        const tareas = inject('tareas')
        const filtro = inject('filtro')
        const long = computed(() =>{
        
        const long = tareas.value.filter(item=> item.estado === false)
            return long.length
        })

        const cleartareas =() =>{
            tareas.value = tareas.value.filter(item=> item.estado === false)
        }

        const clearactive =() =>{
            filtro.value = 'completado'
        }
        const clearcompelte =() =>{
            filtro.value = 'activo'
        }
        const all =() =>{
            filtro.value = '-'
        }

        // console.log(savetareas.value)
        return {tareas, long, cleartareas, clearactive, clearcompelte, all, filtro}
    }
}
</script>

<style scoped>

    .footer{
        display: flex;
        height: 50px;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        padding: 10px;
        box-sizing: border-box;
        border-radius: 2px;
        background-color: white;
    }
    .footer__p{
        font-size: 10px;
    }
    .footer button{
        font-size: 10px;
        outline: none;
        border: none;
        margin: 4px;
        background-color: inherit;
        color: inherit;
        cursor: pointer;
    }
    .footer button:focus{
        color: #5875DF;
    }
    .dark .footer{
        background-color: #25273C;
    }
    button:hover{
        transform: scale(1.03);
        transition: 0.3s linear;
    }
    .dark  .footer button:focus{
        color: violet;
    }
</style>