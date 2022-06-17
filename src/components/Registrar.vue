

<script >

export default {
  name: "Registrar",

  data() {
    return {
      usuarioRegister: {
        nombre: "",
        apellido: "",
        email: "",
        telefono: "",
        password: "",
      },
      repetirPassword: "",
    };
  },
  methods: {
    async insertar() {
      if (this.usuarioRegister.password != this.repetirPassword) {
        alert("Contraseñas incorrectas");
        return;
      }
      var me = this;
      console.log('Insertando...');
 

      const request = await fetch('http://localhost:8080/api/usuarios', {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.usuarioRegister)
      });

      this.usuarioRegister.nombre = "";
      this.usuarioRegister.apellido = "";
      this.usuarioRegister.telefono = "";
      this.usuarioRegister.email = "";
      this.usuarioRegister.password = "";
      this.repetirPassword = "";

      alert("La cuenta fue creada con exito");
    window.location.href='http://localhost:8081/#/';
    },
   
  },
  mounted(){
if (window.localStorage) {
    if (window.localStorage.getItem('token') !== undefined
      && window.localStorage.getItem('token')
    ){
      window.location.href='/#/Mascotas'
    }
  }
  },
   
};
</script>

<template>
<div class="container mt-5">
  <div class="card">
    <div class="card-body">
      <div class="mb-3">
        <label for="nombre" class="form-label">Nombre</label>
        <input
          type="text"
          name=""
          id="nombre"
          class="form-control"
          v-model="usuarioRegister.nombre"
          placeholder="Nombre"
        />
      </div>

      <div class="mb-3">
        <label for="apellido" class="form-label">Apellido</label>
        <input
          type="text"
          class="form-control"
          id="apellido"
          v-model="usuarioRegister.apellido"
          placeholder="Apellido"
        />
      </div>
      <div class="mb-3">
        <label for="emial" class="form-label">E-mail</label>
        <input
          type="text"
          class="form-control"
          id="emial"
          v-model="usuarioRegister.email"
          placeholder="Email"
        />
      </div>
      <div class="mb-3">
        <label for="telefono" class="form-label">Telefono</label>
        <input
          type="text"
          class="form-control"
          id="telefono"
          v-model="usuarioRegister.telefono"
          placeholder="Telefono"
        />
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Password</label>
        <input
          type="password"
          class="form-control"
          id="password"
          v-model="usuarioRegister.password"
          placeholder="Password"
        />
      </div>
      <div class="mb-3">
        <label for="repetirPass" class="form-label">Repertir password</label>
        <input
          type="password"
          class="form-control"
          id="repetirPass"
          v-model="repetirPassword"
          placeholder="Repetir password"
        />
      </div>
      <button type="button" class="btn btn-primary" @click="insertar()">
        Registrar
      </button>
    </div>
  </div>
  </div>
</template>