<script setup>
import { ref, reactive } from 'vue';
import Form from './components/Form.vue';
import Header from './components/Header.vue';
import Patient from './components/Patient.vue';


const pacients = ref([]);

const paciente = reactive({
  nombre: '',
  correo: '',
  fecha: '',
  sintomas: ''
});

const savePacient = () => {
  pacients.value.push({...paciente});
  if (pacients.value.length > 0) {
    Object.assign(paciente, {
      nombre: '',
      correo: '',
      fecha: '',
      sintomas: ''
    })
  }
};
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Form v-model:nombre="paciente.nombre" v-model:correo="paciente.correo" v-model:fecha="paciente.fecha"
        v-model:sintomas="paciente.sintomas" @save-pacient="savePacient" />

      <div class="md:w-1/2 md:h-screen overflow-y-auto scrollbar">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>
        <div v-if="pacients.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Patient v-for="(patient, i) in pacients" :key="i" :patient="patient" />
        </div>
        <p v-else class="mt-10 text-2xl text-center">No Hay Pacientes</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.scrollbar::-webkit-scrollbar {
  display: none; /* Oculta la scrollbar en navegadores basados en WebKit (Chrome, Safari) */
}
.scrollbar {
  -ms-overflow-style: none; /* Oculta la scrollbar en Internet Explorer y Edge */
  scrollbar-width: none; /* Oculta la scrollbar en Firefox */
}
</style>
