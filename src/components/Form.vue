<script setup>
import { reactive } from 'vue';
import Alert from './Alert.vue';

const alert = reactive({
    type: '',
    message: ''
});

const paciente = reactive({
    nombre: '',
    correo: '',
    fecha: '',
    sintomas: ''
});

const validate = () => {
    if (Object.values(paciente).includes('')) {
        alert.message = 'Todos los campos son obligatorios';
        alert.type = 'error';
        return;
    } else {
        alert.message = 'Guardado correctamente';
        alert.type = 'done';
        return;
    }
};

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </p>

        <Alert v-if="alert.message" :alert="alert"/>
        
        <form @submit.prevent="validate" class="bg-white shadow-md rounded-lg py-10 px-5 mb-10">
            <div class="mb-5">
                <label for="paciente" class="block text-gray-700 uppercase font-bold">
                    Nombre paciente
                </label>
                <input type="text" id="paciente" placeholder="Nombre del paciente"
                    class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md"
                    v-model="paciente.nombre">
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Correo electrónico
                </label>
                <input type="email" id="email" placeholder="Corrreo electrónico del paciente"
                    class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md"
                    v-model="paciente.correo">
            </div>
            <div class="mb-5">
                <label for="fecha" class="block text-gray-700 uppercase font-bold">
                    Fecha de consulta
                </label>
                <input type="date" id="fecha" class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md"
                v-model="paciente.fecha">
            </div>
            <div class="mb-5">
                <label for="consulta" class="block text-gray-700 uppercase font-bold">
                    Síntomas
                </label>
                <textarea type="text" id="consulta" placeholder="Detalla los sintomas que presenta"
                    class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md h-30" 
                    v-model="paciente.sintomas"/>
            </div>
            <input type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar paciente" />
        </form>
    </div>
</template>


<style scoped></style>