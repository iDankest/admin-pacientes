<script setup>
import { reactive } from 'vue';
const paciente = reactive({
    nombre: '',
    email: '',
    alta: '',
    sintomas: '',
})

const validando = e => {
    if([paciente.nombre, paciente.email].includes('')){
        document.getElementById('error').innerHTML = 'Todos los campos son obligatorios'
        return
    }
    document.getElementById('error').innerHTML = ''
    console.log(paciente)
}

</script>

<template>
        <div class="md:w-1/2">
            <h2 class="font-black text-3xl text-center">Seguimiento de pacientes</h2>
            <p class="text-lg mt-5 text-center mb-10">
                Añande pacientes y 
                <span class="text-indigo-600 font-bold">Adminístralos</span>
            </p>
            <form class="shadow-md bg-white rounded-lg py-10 px-5 mb-10" @submit.prevent="validando">
                <p id="error" class="text-red-500 mt-5"></p>
                <div class="mb-5">
                    {{ paciente.nombre }}
                    <label for="nombre" class="block text-gray-700 uppercase font-bold">
                        Nombre del paciente
                    </label>
                    <input type="text" v-model="paciente.nombre"  id="nombre" placeholder="Nombre del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md" >
                </div>
                <div class="mb-5">
                    <label for="email" class="block text-gray-700 uppercase font-bold">
                        Email
                    </label>
                    <input type="email" v-model="paciente.email" id="email" placeholder="Email del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md">
                </div>
                <div class="mb-5">
                    <label for="alta" class="block text-gray-700 uppercase font-bold">
                        Alta
                    </label>
                    <input type="date" v-model="paciente.alta" id="alta" placeholder="Alta del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md">
                </div>
                <div class="mb-5">
                    <label for="sintomas" class="block text-gray-700 uppercase font-bold">
                        Síntomas
                    </label>
                    <textarea id="sintomas" v-model="paciente.sintomas" placeholder="Síntomas del paciente" class="border-2 placeholder-gray-400 w-full p-2 mt-2 rounded-md h-40"></textarea>
                </div>
                <input type="submit" value="Agregar paciente" class="w-full bg-indigo-600 hover:bg-indigo-700 transition-colors cursor-pointer text-white font-bold p-2 rounded-md">
            </form>
        </div>
</template>