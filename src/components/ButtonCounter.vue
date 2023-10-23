<script setup>
 import {ref} from 'vue'
 const counter = ref(0)
</script>

<template>
    <button class="btn btn-outline-success" @click="counter++">contador {{ counter }}</button>
</template>