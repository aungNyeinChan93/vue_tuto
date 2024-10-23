
<template>
    <section>
        <h3 class=" text-danger">Test Vue {{ name }}</h3>
        <button @click="change" class="btn btn-sm btn-danger">change</button>
        <div class="container">
            <form @submit.prevent="submit">
                <input type="text" name="text" id="text" class="formcontrol" v-model="form.text">
                <button>add</button>
            </form>
        </div>
    </section>
</template><h3>Test Vue</h3>


<script setup >
import { ref } from 'vue';
import { reactive } from 'vue';


    const name = ref("mgmg")

    const change = ()=>{
        name.value = "aye";
    }

    const form = reactive({
        text:null
    });

    const submit= (e)=>{
        // console.log(e.target.text.value);  
        name.value = e.target.text.value;
        
    }

    
</script>
