<script setup>
    const props = defineProps({
        paciente: {
            type: Object,
            required: true,
        }
    });

    const emit = defineEmits([
        'editar-paciente',
        'eliminar-paciente',
    ]);
</script>
<template>
    <div class="mx-5 mt-5 bg-white shadow-md p-5 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase">ID:
            <span class="font-normal normal-case">
             {{ paciente.id }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Mascota:
            <span class="font-normal normal-case">
                {{ paciente.mascota }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Propietario: 
            <span class="font-normal normal-case">
                {{ paciente.propietario }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Correo electrónico: 
            <span class="font-normal normal-case">
                {{ paciente.email }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Fecha Alta:
            <span class="font-normal normal-case">
                {{ paciente.fecha }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Síntomas:
            <span class="font-normal normal-case">
                {{ paciente.sintomas }}
            </span>
        </p>

        <div class="grid md:grid-cols-2  gap-5 mt-10 ">
            <button
                @click="$emit('editar-paciente', paciente.id)"
                type="button"
                class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
            >Editar</button>

            <button
                @click="$emit('eliminar-paciente', paciente.id)"
                type="button"
                class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
            >Eliminar</button>
        </div>
    </div>
</template>