<script setup>
import { ref, reactive } from 'vue';
import Form from './components/Form.vue';
import Header from './components/Header.vue';

const pacients = ref([]);

const paciente = reactive({
    nombre: '',
    correo: '',
    fecha: '',
    sintomas: ''
});

const savePacient = () => {
  pacients.value.push(paciente);
};
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Form
      v-model:nombre="paciente.nombre" v-model:correo="paciente.correo" v-model:fecha="paciente.fecha" v-model:sintomas="paciente.sintomas" 
      @save-pacient="savePacient"/>

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>
        <div v-if="pacients.length > 0"></div>
        <p v-else class="mt-10 text-2xl text-center">No Hay Pacientes</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
