<template>
    <div class="container">
        <div class="tittle-container">
            <h1 class="tittle-container__tittle">TODO</h1>
            <img :src="require(`../images/${logo}`)"  alt="" role="button" @click="cambiarmodo"  class="tittle-container__image">
        </div>
        <form @submit.prevent="ingresartarea" class="container__form">
                <input type='checkbox' name='thing' value='valuable' id="thing" v-model="estado"/>
                <label for="thing"></label>

                <input 
                type="text"
                placeholder="Create a new todo..."
                v-model.trim="texto"
                class="container__form_text"
                >
                
        </form>
       
    </div>

</template>

<script>
import { inject, ref } from 'vue'
export default {
    props:{
        mode:{
            type:String,
            required:true
        }
    },
    setup(){
        const texto = ref('')   
        const estado = ref(false)   
        const tareas = inject('tareas')
        const mode = inject('mode')
        const logo = ref('icon-moon.svg')


        const ingresartarea = () =>{
                if(texto.value !== ""){
                    let filtro = ''

                    if(estado.value){
                        filtro = 'completado'
                    }
                    else{
                        filtro = 'activo'
                    }

                    const tarea = {
                        'id':Date.now(),
                        'estado':estado.value,
                        'texto': texto.value,
                        'filtro': filtro
                    }
                    tareas.value.push(tarea)

            }

        }
        const cambiarmodo = () =>{
            if(mode.value === 'dark'){
                mode.value = 'light'
                logo.value = 'icon-sun.svg'
            }
            else{
                mode.value = 'dark'
                logo.value = 'icon-moon.svg'
            }
        }
        return {texto, estado, tareas, ingresartarea, cambiarmodo, logo}
    }
}
</script>

<style scoped>
@media (max-width: 4000px){
    .container{
        display: block;
        height: 100%;
        width: 38vw;
        padding: 3rem 30vw;
        /* margin: 100px; */
    }
    .tittle-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 2rem 0;
    }   
}
@media (max-width: 1200px){
    .container{
        display: block;
        height: 100%;
        width: 80vw;
        padding: 0rem 10vw;
        /* margin: 100px; */
    }
    .tittle-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 0;
    }   
}

.tittle-container__tittle{
    color: white;
    font-weight: 300;
    font-size: 35px;
    letter-spacing: 10px;
}
.tittle-container__image{
    cursor: pointer;
}
.container__form{
    display: flex;
    padding: 10px;
    align-items: center;
    box-sizing:border-box;
    width: 100%;
    height: 3rem;
    background-color: whitesmoke;
    border-radius: 10px;
}
.dark .container__form{
    background-color :#25273C;
}

.container__form_checkbox{
    margin: 0rem 10px;
    width: 1em;
    height: 1em;
    background-color: white;
    border-radius: 50%;
    border: 1px solid hsl(234, 11%, 52%);
    vertical-align: middle;
    outline: none;
    cursor: pointer;
    -webkit-appearance: none;
}
.container__form_checkbox:checked{
    background: linear-gradient(hsl(192, 100%, 67%) , hsl(280, 87%, 65%));
  
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

.container__form_text{
    height: 100%;
    width: 100%;
    outline: none;
    border: none;
    background: #F5F5F5;
}
.dark .container__form_text{
    background-color: #25273C;
    color: hsl(234, 39%, 85%);
}
</style>