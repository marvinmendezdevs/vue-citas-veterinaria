<script setup>
  import { reactive, ref, onMounted, watch } from 'vue';
  import { uid } from 'uid';

  import Header from './components/Header.vue';
  import Formulario from './components/Formulario.vue';
  import Paciente from './components/Paciente.vue';

  const pacientes = ref([]);
  const paciente = reactive({
      id: null,
      mascota: '',
      propietario: '',
      email: '',
      fecha: '',
      sintomas: '',
  });

  onMounted(() => {
    const dataLS = localStorage.getItem('pacientes') ?? null;
    if(dataLS){
      pacientes.value = JSON.parse(dataLS);
    }
  });

  watch(pacientes, () => {
    localStorage.setItem('pacientes', JSON.stringify(pacientes.value));
  }, {deep: true});

  const agregarPaciente = () => {
    if(paciente.id){
      const index = pacientes.value.findIndex(pacienteState => pacienteState.id === paciente.id);
      Object.assign(pacientes.value[index], paciente);
    }else{
      paciente.id = uid();
      pacientes.value.push({...paciente});
    }

    Object.assign(paciente, {
      id: null,
      mascota: '',
      propietario: '',
      email: '',
      fecha: '',
      sintomas: '',
    });
  }

  const editarPaciente = id => {
    const pacienteEditar = pacientes.value.find(pacienteState => pacienteState.id === id);
    Object.assign(paciente, pacienteEditar);
  }

  const eliminarPaciente = id => {
    pacientes.value = pacientes.value.filter(pacienteState => pacienteState.id !== id);
  }
</script>

<template>
  <Header />
  <div class="container mx-auto md:flex">
    <Formulario
      v-model:mascota="paciente.mascota"
      v-model:propietario="paciente.propietario"
      v-model:email="paciente.email"
      v-model:fecha="paciente.fecha"
      v-model:sintomas="paciente.sintomas"
      @agregar-paciente="agregarPaciente"
      :id="paciente.id"
    />
    <div class="w-1/2 h-screen overflow-y-auto">
      <h2 class="font-black text-3xl text-center mb-3">Administra tus Pacientes</h2>
        <p class="text-center text-lg">
            Realiza un siguimiento de tus 
            <span class="text-indigo-600 font-bold">pacientes</span>
        </p>
      <Paciente
        v-if="pacientes.length > 0"
        v-for="paciente in pacientes"
        @editar-paciente="editarPaciente"
        @eliminar-paciente="eliminarPaciente"
        :paciente="paciente"
      />
      <p v-else class="text-center text-2xl font-black mt-10">
        No hay pacientes aún
      </p>
    </div>
  </div>
</template>