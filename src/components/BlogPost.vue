<script setup>
    defineProps({
        title:String,
        id:Number,
        body:{
            type:String,
            default:'No description'
        },
        colorText:{
            type:String,
            default:'primary'
        }
    })
    const emit=defineEmits(["myFav"])
   
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`">{{ id }}-{{ title }}</h5>
            <p>{{body}}</p>
            <button class="btn btn-sm btn-outline-primary"
            @click="emit('myfav', title)"> Fav</button>
        </div>
    </div>
</template>