<script setup>
import { ref, reactive, watch, onMounted } from 'vue';
import { uid } from 'uid';
import Form from './components/Form.vue';
import Header from './components/Header.vue';
import Patient from './components/Patient.vue';

const pacients = ref([]);

watch(pacients, () => {
  patientPersistent();
}, {
  deep: true
});

onMounted(() => {
  const patientStorage = localStorage.getItem('patient');
  if (patientStorage) {
    pacients.value = JSON.parse(patientStorage);
  }
});

const paciente = reactive({
  id: null,
  nombre: '',
  correo: '',
  fecha: '',
  sintomas: ''
});

const savePacient = () => {
  if (paciente.id) {
    const {id} = paciente;
    const i = pacients.value.findIndex((patientState) => patientState.id === id);
    pacients.value[i] = {...paciente};
  } else {
    pacients.value.push({
    ...paciente,
    id: uid()
  });
  }
  
  if (pacients.value.length > 0) {
    Object.assign(paciente, {
      nombre: '',
      correo: '',
      fecha: '',
      sintomas: '',
      id: null
    })
  };
};

const updatePatient = (id) => {
  const modifyPatient = pacients.value.filter(paciente => paciente.id === id)[0];
  Object.assign(paciente, modifyPatient);
};

const deletePatient = (id) => {
  pacients.value = pacients.value.filter(paciente => paciente.id !== id);
};

const patientPersistent = () => {
  localStorage.setItem('patient', JSON.stringify(pacients.value));
}
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Form v-model:nombre="paciente.nombre" v-model:correo="paciente.correo" v-model:fecha="paciente.fecha"
        v-model:sintomas="paciente.sintomas" @save-pacient="savePacient" :id="paciente.id"/>

      <div class="md:w-1/2 md:h-screen overflow-y-auto scrollbar">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>
        <div v-if="pacients.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Patient v-for="(patient, i) in pacients" :key="i" :patient="patient" @update-patient="updatePatient" @delete-patient="deletePatient"/>
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
