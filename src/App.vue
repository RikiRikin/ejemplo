<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Bienvenido</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavAltMarkup" >
      <div class="navbar-nav" >
        <a class="nav-link active" aria-current="page" href="#/Mascotas">Mascotas</a>
        <!-- <a class="nav-link active" aria-current="page" href="#/registrar">Registrar</a> -->
        <a class="nav-link active"  aria-current="page" @click="salir()" href="#/">Cerrar sesion</a>
      </div>
      <div class="navbar-nav" >
        <a class="nav-link active" aria-current="page" href="#/">Iniciar sesion</a>
        <a class="nav-link active" aria-current="page" href="#/registrar">Registrar</a>
      </div>
    </div>
  </div>
</nav>
  <component :is="currentView" />
</template>

<script>

import Mascotas from "./components/Mascotas.vue";
import Login from "./components/Login.vue";
import Registrar from "./components/Registrar.vue";
import MascotaModificar from "./components/MascotaModificar.vue";
import MascotasRegistrar from "./components/MascotasRegistrar.vue";

const routes = {
  '/': Login,
  '/Mascotas': Mascotas,
  '/registrar': Registrar,
  '/Mascotas/registrar': MascotasRegistrar,
  '/Mascotas/modificar': MascotaModificar,
}

export default {
  data() {
    return {
      currentPath: window.location.hash,
      // estado: "Iniciar sesion",
      navStatus: true
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
		  this.currentPath = window.location.hash
		})
  //   if (window.localStorage) {
  //   if (window.localStorage.getItem('token') !== undefined
  //     && window.localStorage.getItem('token')
  //   ){
  //     this.navStatus = true
  //   }else{
  //     this.navStatus = false
  //   }
  // }else{
  //     this.navStatus = false
  //   }

    
  },
  methods: {
   salir(){
localStorage.removeItem('token');
this.navStatus = true
   },
  },
 
  
}

// export default {
//   name: "App",
//   components: {
//     Mascotas,
//   },
// };
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
