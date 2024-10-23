<template>
    <section>
        <div class="container">
            <form @submit.prevent="addTask">
                <div class="mt-3 btn-group mb-3">
                    <input type="text" name="task" id="task" class="formcontrol" v-model="form.task" on-focus >
                <button class="btn btn-sm btn-primary">Add</button>
                </div>
            </form>
            <div class="card">
                <ul>
                    <div  v-for="(task,index) in tasks" :key="index" class=" d-flex  justify-content-between px-3 py-1">
                        <li :class="{'delete':task.status , 'red':!task.status}">{{ task.task }}</li>
                        <input type="checkbox" v-model="task.status">
                    </div>
                </ul>
            </div>
            <button class="btn btn-sm btn-danger my-2 " @click="hideStatus "  >Clear</button>
        </div>
    </section>
</template>

<script setup>
import { reactive, ref } from 'vue';

    const hideAction = ref(false);

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


    const addTask = (e)=>{
        console.log(e.target[0].value);
        let data = {
            task:e.target.task.value,
            status:false,
        }
        tasks.value.push(data);
        form.task = "";
    }

    const hideStatus=()=>{
        if(!hideAction.value){
            tasks.value = tasks.value.filter((task)=>{
                return !task.status ;
            });
        }
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