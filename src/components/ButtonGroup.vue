<script setup>
   const emit=defineEmits(["paginatePrev", "paginateNext"])
   defineProps(["init","end","maxLength"])
</script>

<template>
    <div class="btn-group">
 <button @click="emit('paginatePrev')" class="btn btn-outline-primary" :disabled="init<=0" >Previous</button>
 <button  @click="emit('paginateNext')" class="btn btn-outline-primary" :disabled="end>=maxLength">Next</button>
</div>
</template>