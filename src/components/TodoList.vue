<template>
    <section>
        <div class="container">
            <h3 class="p-2 bg-info text-white my-1 text-center rounded ">Todo List </h3>
            <form @submit.prevent="addTask">
                <div class="mt-3 btn-group mb-3">
                    <input type="text" name="task" id="task" class="formcontrol" v-model="form.task" on-focus  >
                    <button class="btn btn-sm btn-primary ms-2">Add</button> 
                    <input type="checkbox" name="check_status" id="check_status" v-model="checkStatus" class="mx-2">
                    <input type="file" name="image" id="" @change="change" disabled>
                    <img :src="imagePreview" class=" img-fluid w-25" alt="" >
                    <input type="checkbox" name="view" id="view" v-model="view" @change="view_hide"><span class="mx-2">Hide </span>
                </div>
            </form>

            <div v-show="tasks.length == 0" class="alert alert-success">Empty Task</div>
            <div class="card" v-show="tasks.length >0">
                <ul>
                    <div  v-for="(task,index) in tasks" :key="index" class=" d-flex  justify-content-between px-3 py-1">
                        <li :class="{'delete':task.status , 'red':!task.status}">{{ task.task }}</li>
                        <input type="checkbox" v-model="task.status">
                    </div>
                </ul>
            </div>
            <button class="btn btn-sm btn-danger my-2 " @click="clear">Clear</button>
        </div>
    </section>
</template>

<script setup>

import { onMounted, reactive, ref } from 'vue';

    const hideAction = ref(false);

    const checkStatus = ref(false);

    const imagePreview = ref();

    const view = ref(false);


    const tasks= ref([
        {
            task:"CSS",
            status:false
        },
        {
            task:"JS",
            status:true
        },
        {
            task:"HTML",
            status:true
        },
    ]);

    const form = reactive({
        task:null,
    });

    // onBeforeUnmount(()=>{
    //     if(localStorage.getItem("localTasks")){
    //         onMounted();
    //     }
    // });

    onMounted(()=>{
       if(localStorage.getItem("localTasks")){
        const localData = (localStorage.getItem("localTasks"));
        tasks.value = JSON.parse(localData);
       }
    });
   
    const addTask = (e)=>{
        console.log(e.target.image.value);
        if(form.task !== ""){
                let data = {
                task:e.target.task.value,
                status:checkStatus.value,
            }
            tasks.value.push(data);
            localStorage.setItem("localTasks",JSON.stringify(tasks.value));
            form.task = "";
            // location.reload();
        }else{
            alert("can't be null value!");
        }
    }

    const clear=()=>{
        if(!hideAction.value){
            tasks.value = tasks.value.filter((task)=>{
                return !task.status
            })
            localStorage.setItem("localTasks",JSON.stringify(tasks.value))   
        }
    }

    const change = (e)=>{
        console.log(e.target.files[0].name);
        imagePreview.value = URL.createObjectURL(e.target.files[0]);
    }

    const view_hide = ()=>{
        tasks.value = view.value ? tasks.value.filter(task=>!task.status) : tasks.value;
    }


</script>

<style>
    .delete{
        text-decoration: line-through;
        font-style: italic;
    }
    .red{
        color: rgba(219, 43, 43, 0.747);
    }
</style>