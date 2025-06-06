<script setup>
import { reactive, computed } from 'vue';
import Alerta from './Alerta.vue';

const alerta= reactive({
    tipo: '',
    mensaje: ''
})

const emit = defineEmits(['update:nombre', 'update:email', 'update:alta', 'update:sintomas', 'agregar-paciente'])//Emits para pasar info al padre

const props = defineProps({ //Props para recibir info del padre mostrar la info en el Dom
    id:{
        type: [String, null],
        required: true
    },
    nombre:{
        type: String,
        required: true
    },
    email:{
        type: String,
        required: true
    },
    alta:{
        type: String,
        required: true
    },
    sintomas:{
        type: String,
        required: true
    }
})

const validando = e => {
    if(Object.values(props).includes('')){//Object.values() Devuelve los valores del objetos permitiendo que se mas facil escalar
        alerta.mensaje='Toddos los campos son obligatorios'
        alerta.tipo='error'
        return
    }
    emit('agregar-paciente')
    alerta.mensaje='Paciente agregado correctamente'
    alerta.tipo='exito'
    setTimeout(() => {
        alerta.mensaje=''
        alerta.tipo=''
    }, 3000)
}

const editando = computed(() => {
    return props.id //Esto nos retorna true o false
})
</script>

<template>
        <div class="md:w-1/2">
            <h2 class="font-black text-3xl text-center">Seguimiento de pacientes</h2>
            <p class="text-lg mt-5 text-center mb-10">
                Añande pacientes y 
                <span class="text-indigo-600 font-bold">Adminístralos</span>
            </p>
            <Alerta 
            v-if="alerta.mensaje"
            :alerta="alerta"
            />
            <form class="shadow-md bg-white rounded-lg py-10 px-5 mb-10" @submit.prevent="validando">
                <p id="error" class="text-red-500 mt-5"></p>
                <div class="mb-5">
                    <label for="nombre" class="block text-gray-700 uppercase font-bold">
                        Nombre del paciente
                    </label>
                    <input type="text" :value="nombre" @input="$emit('update:nombre', $event.target.value)" id="nombre" placeholder="Nombre del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md" >
                </div>
                <div class="mb-5">
                    <label for="email" class="block text-gray-700 uppercase font-bold">
                        Email
                    </label>
                    <input type="email" :value="email" @input="$emit('update:email', $event.target.value)" id="email" placeholder="Email del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md">
                </div>
                <div class="mb-5">
                    <label for="alta" class="block text-gray-700 uppercase font-bold">
                        Alta
                    </label>
                    <input type="date" :value="alta" @input="$emit('update:alta', $event.target.value)" id="alta" placeholder="Alta del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md">
                </div>
                <div class="mb-5">
                    <label for="sintomas" class="block text-gray-700 uppercase font-bold">
                        Síntomas
                    </label>
                    <textarea :value="sintomas" @input="$emit('update:sintomas', $event.target.value)" id="sintomas" placeholder="Síntomas del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md h-40"></textarea>
                </div>
                <input type="submit" :value="[editando ? 'guardar cambios' : 'agregar paciente']" class="w-full bg-indigo-600 hover:bg-indigo-700 transition-colors cursor-pointer text-white font-bold p-2 rounded-md">
            </form>
        </div>
</template>