<template>
    <div>
      <img 
        height="100px" 
        :src="foto" 
        :alt="email" 
        @click="emitirImagenClick" 
        style="cursor: pointer;"
      />
      <button @click="emitirEliminar">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      nombre: String,
      email: String,
      foto: String
    },
    methods: {
      emitirEliminar() {
        this.$emit('eliminar');
      },
      emitirImagenClick() {
        this.$emit('imagenClick');
      }
    }
  };
  </script>
  