<script
 setup lang="ts">

import { ref } from 'vue'

defineProps<{ msg: string }>()

const nombre = ref("")
const contrasenia = ref("")
const correo = ref("")
const nacimiento = ref("")

function calcularEdad(fechaNacimiento: string): number {
  const hoy = new Date();
  const nacimientoDate = new Date(fechaNacimiento);
  let edad = hoy.getFullYear() - nacimientoDate.getFullYear();
  const mes = hoy.getMonth() - nacimientoDate.getMonth();
  if (mes < 0 || (mes === 0 && hoy.getDate() < nacimientoDate.getDate())) {
    edad--;
  }
  return edad;
}

function guardarDatos(){
  if (nombre.value && contrasenia.value && correo.value && nacimiento.value){
    const edad = calcularEdad(nacimiento.value);
    
    alert("Usuario creado correctamente!\nNombre: " + nombre.value + "\nCorreo: " + correo.value + "\nFecha de nacimiento: " + nacimiento.value + "\nEdad: " + edad);
    
    console.log({
      nombre: nombre.value,
      contrasenia: contrasenia.value,
      correo: correo.value,
      nacimiento: nacimiento.value,
      edad: edad
    });
    
    nombre.value = "";
    contrasenia.value = "";
    correo.value = "";
    nacimiento.value = "";
  } else {
    alert("Debe completar los campos");
  }
}
</script>

<template>

  <div class="form-container">

    <h1>{{ msg }}</h1>
      <form @submit.prevent="guardarDatos">
        <h2>Nuevo Usuario</h2>
        <input type="text" placeholder="Escribe tu nombre" v-model="nombre">
        <input type="password" placeholder="Escribe tu contraseña" v-model="contrasenia">
        <input type="email" placeholder="Escribe tu email" v-model="correo">
        <input type="date" v-model="nacimiento">
        <button type="submit">Guardar</button>
      </form>
  </div>


</template>

<style scoped>


</style>