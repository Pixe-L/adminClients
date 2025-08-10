<script setup>
import { reactive } from 'vue';
import Alert from './Alert.vue';

const alert = reactive({
    type: '',
    message: ''
});

const emit = defineEmits(['update:nombre', 'update:correo', 'update:fecha', 'update:sintomas', 'save-pacient']);

const props = defineProps({
    nombre: {
        type: String,
        required: true
    },
    correo: {
        type: String,
        required: true
    },
    fecha: {
        type: String,
        required: true
    },
    sintomas: {
        type: String,
        required: true
    }
});

const validate = () => {
    if (Object.values(props).includes('')) {
        alert.message = 'Todos los campos son obligatorios';
        alert.type = 'error';
    } else {
        alert.message = 'Guardado correctamente';
        alert.type = 'done';
        emit('save-pacient')
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
                    class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md" @input="$emit('update:nombre', $event.target.value)"
                    :value="nombre">
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Correo electrónico
                </label>
                <input type="email" id="email" placeholder="Corrreo electrónico del paciente"
                    class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md" @input="$emit('update:correo', $event.target.value)"
                    :value="correo">
            </div>
            <div class="mb-5">
                <label for="fecha" class="block text-gray-700 uppercase font-bold">
                    Fecha de consulta
                </label>
                <input type="date" id="fecha" class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md" @input="$emit('update:fecha', $event.target.value)"
                :value="fecha">
            </div>
            <div class="mb-5">
                <label for="consulta" class="block text-gray-700 uppercase font-bold">
                    Síntomas
                </label>
                <textarea type="text" id="consulta" placeholder="Detalla los sintomas que presenta"
                    class="border-2 w-full p-2 mt-2 placeholder-indigo-400 rounded-md h-30" @input="$emit('update:sintomas', $event.target.value)"
                    :value="sintomas"/>
            </div>
            <input type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar paciente" />
        </form>
    </div>
</template>


<style scoped></style>