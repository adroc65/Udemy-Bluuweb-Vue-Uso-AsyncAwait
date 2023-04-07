<script setup>

    defineProps(['inicio', 'fin', 'maxLength']);
    const emit = defineEmits(['next', 'prev']);

</script>

<template>
    <div class="btn-group m-2" role="group" aria-label="Basic outlined example">
        <button
            @click="emit('prev')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="inicio <= 0"
            >Previus <span>{{ inicio }}</span>
        </button>
        <button 
            @click="emit('next')"
            type="button" 
            class="btn btn-outline-primary"
            :disabled="fin >= maxLength "
            >Next <span>{{ fin }}</span>
        </button>
    </div>
</template>