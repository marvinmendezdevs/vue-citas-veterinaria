<script setup>
    import { computed } from 'vue';
    const props = defineProps({
        alerta : {
            type: Object,
            required: true,
        }
    });

    const tipo = computed(() => {
        return props.alerta.tipo === 'error' ? 'bg-red-500' : 'bg-green-500';
    });
</script>

<template>
    <div :class="tipo" class="mb-3 text-center text-white p-1 rounded">
        {{alerta.mensaje}}
    </div>
</template>
