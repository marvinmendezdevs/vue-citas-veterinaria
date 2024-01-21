<script setup>
    import { reactive, computed } from 'vue';
    import Alerta from './Alerta.vue';

    const emit = defineEmits([
        'update:mascota',
        'update:propietario',
        'update:email',
        'update:fecha',
        'update:sintomas',
        'agregar-paciente',
    ]);
    const props = defineProps({
        id: {
            type: [String, null],
            required: true,
        },
        mascota: {
            type: String,
            required: true,
        },
        propietario: {
            type: String,
            required: true,
        },
        email: {
            type: String,
            required: true,
        },
        fecha: {
            type: String,
            required: true,
        },
        sintomas: {
            type: String,
            required: true,
        },
    });

    const alerta = reactive({
      mensaje: '',
      tipo: '',
    });

    const validarFormulario = () => {
      if(Object.values(props).includes('')){
        alerta.mensaje = 'Todos los campos son obligatorios';
        alerta.tipo = 'error';

        return;
      }

        emit('agregar-paciente');
        alerta.mensaje = props.id ? 'Paciente actualizado correctamente':'Paciente agregado correctamente';
        alerta.tipo = 'exito';

        setTimeout(() => {
            alerta.mensaje = '';
        },3000);
    }

    const cambios = computed(() => {
        return props.id ? 'Actualizar registro' : 'Agregar registro';
    });
</script>

<template>
    <div class="md:w-1/2 p-5 md:p-0">
        <h2 class="font-black text-3xl text-center mb-3">Seguimiento de Pacientes</h2>
        <p class="text-center text-lg mb-5">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">adminístralos</span>
        </p>

        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />
        <form class="bg-white p-5 shadow-md rounded-lg" @submit.prevent="validarFormulario">
            <div class="mb-5">
                <label class="uppercase font-bold text-gray-700 block mb-1" for="mascota">Mascota:</label>
                <input class="border p-2 w-full rounded-lg" type="text" id="mascota" placeholder="Nombre de la mascota"
                    @input="$emit('update:mascota', $event.target.value)"
                    :value="mascota"
                >
            </div>

            <div class="mb-5">
                <label class="uppercase font-bold text-gray-700 block mb-1" for="propietario">Propietario:</label>
                <input class="border p-2 w-full rounded-lg" type="text" id="propietario" placeholder="Nombre del propietario"
                    @input="$emit('update:propietario', $event.target.value)"
                    :value="propietario"
                >
            </div>

            <div class="mb-5">
                <label class="uppercase font-bold text-gray-700 block mb-1" for="email">Correo electrónico:</label>
                <input class="border p-2 w-full rounded-lg" type="email" id="email" placeholder="Correo electrónico"
                    @input="$emit('update:email', $event.target.value)"
                    :value="email"
                >
            </div>

            <div class="mb-5">
                <label class="uppercase font-bold text-gray-700 block mb-1" for="fecha">Fecha de alta:</label>
                <input class="border p-2 w-full rounded-lg" type="date" id="fecha"
                    @input="$emit('update:fecha', $event.target.value)"
                    :value="fecha"
                >
            </div>

            <div class="mb-5">
                <label class="uppercase font-bold text-gray-700 block mb-1" for="sintomas">Síntomas:</label>
                <textarea class="border p-2 w-full rounded-lg" type="text" id="sintomas" placeholder="Escribe los síntomas"
                    @input="$emit('update:sintomas', $event.target.value)"
                    :value="sintomas"
                />
            </div>

            <input class="bg-indigo-600 w-full p-2 text-white rounded-lg hover:bg-indigo-700 cursor-pointer" type="submit" :value="cambios">
        </form>
    </div>
</template>
