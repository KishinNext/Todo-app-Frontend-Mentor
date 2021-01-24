<template>

    <div class="listtareas" v-if="tarea.filtro !== filtro">
        <input type='checkbox' name='thing' value='valuable' :id="tarea.id" @click="changeEstado(tarea.id)" :checked="checkestado(tarea)"/>
        <label :for="tarea.id"></label>
        <p :class="{'tachado':tarea.estado}">{{tarea.texto}}</p>
        <img src="../images/icon-cross.svg" alt="crossIcon" role="button" class="tableimg" @click="eliminartarea(tarea.id)">
    </div>
</template>

<script>
import { inject, ref } from 'vue'
export default {
    props:{
        tarea:{
            type: Object,
            required: true
        },
        index:{
            type:String,
        }
    },
    setup(){
        const tareas = inject('tareas')
        const filtro = inject('filtro')


        const changeEstado = (id) =>{

            tareas.value = tareas.value.map( item =>{
                if(item.id == id){
                    item.estado = !item.estado
                    if(item.estado){
                        item.filtro = 'completado'
                    }
                    else{
                        item.filtro = 'activo'
                    }
                }
                return item
            })

        }
        const eliminartarea =(id)=>{
            tareas.value = tareas.value.filter(item => item.id !== id)
        }
        const checkestado = (tarea)=>{


            if (tarea.estado === true){
                return "checked"
            }

        }
        return {tareas, changeEstado, eliminartarea, checkestado, filtro}
    }
}
</script>

<style scoped>


    .listtareas{
        display: flex;
        height: 50px;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        padding: 10px;
        box-sizing: border-box;
        background-color: white;
        border-radius: 2px;
        border-bottom:1px solid  hsl(236, 9%, 61%);
    }
    .listtareas:hover{
        background-color: #e9eafa;
    }
    .dark .listtareas:hover{
        background-color: #393A4C;
    }
    .dark .listtareas{
        background-color: #25273C;
    }
    .tachado{
        text-decoration: line-through;
    }
    .tableimg{
        cursor: pointer;

    }


    input[type=checkbox] {
        display:none;
    }

    input[type=checkbox] + label {
        /* background-color: white; */
        margin: 0rem 10px;
        width: 1em;
        height: 1em;
        border-radius: 50%;
        border: 1px solid hsl(234, 11%, 52%);
        display:inline-block;
        padding: 0 0 0 0px;
    }

    input[type=checkbox]:checked + label {
        background-image: url("../images/icon-check.svg");
        background-repeat: no-repeat;
        background-position: center;
        border-radius: 50%;
        border: 1px solid hsl(234, 11%, 52%);
        background-color:#A978F7;
    }
</style>