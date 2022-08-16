<template>
    <div class="container">
        <div class="flex1">
            <div class="card-container">
                <template v-if="taskList.length > 0">
                    <div class="card" v-for="(tarea,index) in taskList" :key="index" >
                        <h4>{{tarea.id}} - {{tarea.titulo}}</h4>
                        <p>{{tarea.info}}</p>
                        <div class="btn-container" >
                            <button class="edit btn" @click="edit(index)">Editar</button>
                            <button class="delete btn" @click="deleteTask(tarea.id)">Eliminar</button>
                        </div>
                    </div>
                </template>
                <div v-else>
                    <p>Aun no hay nada creado puto</p>
                </div>
            </div>
        </div>
        <div class="flex2">
            <div class="agg_container">
                <form @submit.prevent="addTask" v-if="formAgg">
                    <label for="">Titulo de la tarea</label>
                    <input type="text" v-model="inputTitle">
                    <label for="">Descripcion de la tarea</label>
                    <textarea v-model="textareaInfo"></textarea>
                    <button type="submit">Agregar tarea</button>
                </form>
                <form @submit.prevent="editTask()" v-if="!formAgg">
                    <label for="">Titulo de la tarea</label>
                    <input type="text" v-model="inputTitle">
                    <label for="">Descripcion de la tarea</label>
                    <textarea v-model="textareaInfo"></textarea>
                    <button class="edit" type="submit">Editar tarea</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default{

    data(){
        return{
            taskList:[],
            qlo:"mira mmgvo",
            count:1,
            inputTitle:'',
            textareaInfo:'',
            formAgg:true,
            idEdit:'',
        }
    },
    methods:{
        counter(count){
            return this.count ++
        },
        addTask(){
            if(this.inputTitle!=="" && this.textareaInfo !== ""){
                this.taskList.push({
                    id:this.counter(),
                    titulo:this.inputTitle,
                    info: this.textareaInfo,
                    
                })
                let msg= alertify.success('Tarea agregada')
                alertify.set('notifier','position', 'top-right')
                msg.delay(1.5)
            }else{
                Swal.fire({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Rellene los campos',
                    timer: 2000,
                })
            }
            this.inputTitle=''
            this.textareaInfo=''
        },
        deleteTask(id){
            this.taskList = this.taskList.filter((item)=> item.id !== id)
            alertify.success('Tarea eliminada',1.5,'position', 'top-right' )
        },
        edit(id){
            this.formAgg=false;
            this.inputTitle= this.taskList[id].titulo;
            this.textareaInfo= this.taskList[id].info
            this.idEdit= id
        },
        editTask(id){
            this.taskList[this.idEdit].titulo=this.inputTitle;
            this.taskList[this.idEdit].info= this.textareaInfo;
            this.formAgg=true;
            alertify.success('Editado con exito',1.5,'position', 'top-right' )
            this.textareaInfo=''
            this.inputTitle=''
        }
    }
}
</script>

<style scoped>
    .container{
        max-width: 1200px;
        margin: 0 auto;
        min-height: 100px;
        margin-top: 20px;
        display: flex;
        gap: 1em;
    }
    .flex1{
        flex:1.8;
    }
    .flex2{
        flex:1;
    }
    .card{
        padding:10px;
        margin-bottom: 10px;
        display:flex;
        gap: 1em;
        flex-direction: column;
        border-radius: 6px;
        background-color: #fff;
        box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.349);
    }
    h4{
        display: inline;
    }
    .btn-container{
        display: flex;
        gap: 1em;
    }
    .btn{
        padding: 8px 18px;
        border:none;
        color:#fff;
        border-radius: 4px;
        cursor:pointer;
        box-shadow:1px 1px 2px rgba(0, 0, 0, 0.411);
    }
    .delete{
        background: rgb(253, 68, 68);
    }
    .edit{
        background-color: rgb(255, 187, 0);
    }
    p{
        text-align: justify;
    }
    form{
        display: flex;
        flex-direction: column;
        padding:20px;
        background: #fff;
        border-radius:4px;
        gap:.8em;
        box-shadow:2px 2px 4px rgba(0, 0, 0, 0.349);
    }
    input{
        border:none;
        border-bottom:1px solid rgb(250, 37, 118);
        outline:none
    }
    textarea{
        resize: none;
        height: 80px;
        border:none;
        border-bottom:1px solid rgb(250, 37, 118);
        outline:none
    }
    button{
        color: white;
        background-color:rgb(0, 224, 86);
        border: none;
        padding: 10px 0;
        cursor:pointer;
        border-radius: 4px;
    }
</style>
