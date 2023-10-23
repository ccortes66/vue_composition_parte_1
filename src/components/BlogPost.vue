<script setup>
//defineProps(['title','content','id'])
defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default:"Default content" 
    }
})

const emit = defineEmits(['favoritePostName'])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title"> {{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button class="btn btn-outline-primary"  @click="emit('favoritePostName',title)">Favorito</button>
        </div>
    </div>
</template>