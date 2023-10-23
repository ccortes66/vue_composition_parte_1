<script setup>

defineProps(['inicio','fin','largo'])
const emit = defineEmits(['prev','next'])

</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button @click="emit('prev')" :disabled="inicio<=0" type="button" class="btn btn-outline-primary">Previous</button>
        <button @click="emit('next')" :disabled="fin>=largo"  type="button" class="btn btn-outline-primary">Next</button>
    </div>
</template>