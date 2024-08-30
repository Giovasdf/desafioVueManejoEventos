<template>
  <div id="app">
    <div class="container">
      <div class="formulario">
        <h1>Formulario de Usuarios</h1>
        <form @submit.prevent="agregarUsuario">
          <div>
            <label for="nombre">Nombre:</label>
            <input v-model="nuevoUsuario.nombre" type="text" id="nombre" />
          </div>
          <div>
            <label for="email">Email:</label>
            <input v-model="nuevoUsuario.email" type="email" id="email" />
          </div>
          <div>
            <label for="foto">Foto:</label>
            <input v-model="nuevoUsuario.foto" type="text" id="foto" />
          </div>
          <button type="submit">Agregar Usuario</button>
          <button type="button" @click="limpiarCampos">Limpiar</button>
        </form>

        <div v-for="(usuario, index) in usuarios" :key="usuario.email" class="usuario">
          <Persona 
            :nombre="usuario.nombre" 
            :email="usuario.email" 
            :foto="usuario.foto"
            @imagenClick="mostrarDetalles(usuario)"
            @eliminar="eliminarUsuario(index)"
          />
        </div>
      </div>

      <div class="detalles" v-if="usuarioSeleccionado">
        <p><img :src="usuarioSeleccionado.foto" alt="Foto" height="200px" /></p>
        <p>{{ usuarioSeleccionado.nombre }}</p>
        <p> {{ usuarioSeleccionado.email }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Persona from './components/Persona.vue';

export default {
  data() {
    return {
      nuevoUsuario: {
        nombre: '',
        email: '',
        foto: ''
      },
      usuarios: [],
      usuarioSeleccionado: null
    };
  },
  components: {
    Persona
  },
  methods: {
    agregarUsuario() {
      if (this.nuevoUsuario.nombre && this.nuevoUsuario.email && this.nuevoUsuario.foto) {
        this.usuarios.push({ ...this.nuevoUsuario });
        this.limpiarCampos();
      } else {
        alert('Por favor, completa todos los campos.');
      }
    },
    limpiarCampos() {
      this.nuevoUsuario.nombre = '';
      this.nuevoUsuario.email = '';
      this.nuevoUsuario.foto = '';
    },
    eliminarUsuario(index) {
      this.usuarios.splice(index, 1);
      if (this.usuarioSeleccionado && this.usuarioSeleccionado.email === this.usuarios[index]?.email) {
        this.usuarioSeleccionado = null;
      }
    },
    mostrarDetalles(usuario) {
      this.usuarioSeleccionado = usuario;
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
}

.formulario {
  flex: 1;
  margin-right: 20px;
}


.detalles {
  flex: 1;
}

.usuario {
  margin-bottom: 10px;
}

button {
  margin-right: 1em;
}
</style>
