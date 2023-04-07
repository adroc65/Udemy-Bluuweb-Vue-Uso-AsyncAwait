<script setup>
//defineProps(['title', 'id', 'body', 'bgColor', 'textColor'])
defineProps({
    title: {
        type: String,
        default: "No hay titulo!",
    },
    id: Number,
    bgColor: {
        type: String,
        default: "success"
    },
    textColor: {
        type: String,
        default: "dark"
    },
    body: {
        type: String,
        default: "No hay descripcion!"
    }
});

</script>

<template>
    <div 
        class="card mt-2 p-2"
        :class="`bg-${bgColor}`"
        >
        <h5 
            class="card-title"
            :class="`text-${textColor}`"
            > {{ id }}- {{ title }} 
        </h5>
        <p
            :class="`text-${textColor}`"
            > {{ body }}
        </p>
        <button
            @click="$emit('cambiarFavorito', title, id)"
            type="button" 
            class="btn btn-info"
            >Favorito
        </button>

    </div>
</template>