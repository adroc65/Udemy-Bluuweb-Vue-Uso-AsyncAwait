<script setup>
import { ref } from 'vue';

    const counter = ref(0);
    const increment = () => counter.value++
</script>

<template>
    <div class="container">
        <h2>Contador = {{ counter }}</h2>
        <button type="button" class="btn btn-primary btn-lg" @click="increment">+1</button>
    </div>  
</template>