<script setup>
import {ref, reactive} from 'vue'
  import Header from "./components/Header.vue";
  import Formulario from "./components/Formulario.vue";
  import Paciente from "./components/Paciente.vue";

const pacientes = ref([])

const paciente = reactive({
    nombre: '',
    email: '',
    alta: '',
    sintomas: '',
})

const agregarPaciente = () => {
  pacientes.value.push(paciente)
}

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex md:justify-between">
      <Formulario 
      v-model:nombre="paciente.nombre"
      v-model:email="paciente.email"
      v-model:alta="paciente.alta"
      v-model:sintomas="paciente.sintomas"
      @agregar-paciente="agregarPaciente"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
                Información de 
                <span class="text-indigo-600 font-bold">Pacientes</span>
            </p>
          <Paciente
          v-for="paciente in pacientes"
          :key="paciente.id"
          :paciente="paciente"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>
