<template>
  <div class="container mt-5">
    <div class="card">
    <div class="card-body">
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
        <label for="password" class="form-label">Password</label>
        <input
          type="password"
          class="form-control"
          id="password"
          v-model="usuarioRegister.password"
          placeholder="Password"
        />
      </div>
      <button type="button" class="btn btn-primary" @click="ingresar()">
        Iniciar sesion
      </button>
    </div>
  </div>
  </div>
</template>

<script >

// const axios = require('axios');
export default {
  name: "Registrar",

  data() {
    return {
      usuarioRegister: {
        email: "",
        password: "",
      },
      repetirPassword: "",
    };
  },
  methods: {
    async ingresar() {
      const request = await fetch('http://localhost:8080/api/login', {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.usuarioRegister)

      });
      //const respuesta = await request.json();
      const respuesta = await request.text();

      if(respuesta != "FAIL"){
      localStorage.token = respuesta;
        window.location.href='http://localhost:8081/#/Mascotas'
      }else{
        alert('Credenciales incorrectas')
      }
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