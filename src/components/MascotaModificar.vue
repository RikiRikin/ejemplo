<template>
  
  <section>
    
    <div class="container mt-4">
      <h3>Modificar</h3> <br>
      <div class="card">
        <div class="card-body">
          <div class="mb-3">
            <!-- {{busacarmascota[0].nombre}}
            {{busacarmascota.nombre}} -->
            <label for="nombre" class="form-label">Nombre</label>
            <input type="text" name="" id="nombre" class="form-control" v-model="busacarmascota.nombre"
              placeholder="Nombre mascotas"  > 
              
          </div>
          
          <div class="mb-3">
            <label for="edad" class="form-label">Edad</label>
            <input type="text" class="form-control" id="edad" v-model="busacarmascota.edad" placeholder="Edad mascota">
          </div>
          <div class="mb-3">
            <label for="raza" class="form-label">Raza</label>
            <input type="text" class="form-control" id="raza" v-model="busacarmascota.raza" placeholder="Raza mascota">
          </div>
          <button type="button"  class="btn btn-primary" @click="insertar(busacarmascota.id)">Guardar</button>
          <button type="button"   class="btn btn-danger ms-4" @click="redirigir()">Cancelar</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script >

export default {
  name: "Mascotas",
  created() {
    // fetch("http://localhost:8080/Mascotas")
    fetch("https://lic-gamma.000webhostapp.com/public/mascotas/")
      .then((response) => response.json())
      .then((data) => (this.mascotas = data));
  },

  data() {
    return {
      
      segundamascotas: [],
      segu: [],
      busacarmascota:{
      },
      buscarmstatus:false ,
      insert: false,
      statusform: "Mascotas",
      mascota: {
        
        nombre: "",
        edad: 0,
        raza: ""
      },
    };
  },
  methods: {

    async buscar(id){
      const request = await fetch('http://localhost:8080/api/mascotas/'+id, {
        method: 'GET',
        headers: {'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': localStorage.token},
      });
      this.busacarmascota = await request.json();


      console.log(this.busacarmascota);
    },

    
    async insertar() {
      var me = this;
      
      const request = await fetch('http://localhost:8080/api/mascotas/modificar', {
        method: 'PUT',
        headers: {'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': localStorage.token},
        body: JSON.stringify(me.busacarmascota)
      });

        localStorage.removeItem("Id");
      // this.mascota.id=0;
      this.mascota.nombre="";
      this.mascota.edad=0;
      this.mascota.raza="";

        this.redirigir();
    },
    redirigir(){
      window.location.href='http://localhost:8081/#/Mascotas'
    },
    async llenaMascotas() {
      

      const request = await fetch('http://localhost:8080/api/mascotas', {
        method: 'GET',
        headers: {'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': localStorage.token},
      }); 
      if (!request.ok) {
        // console.log('fuera');
        window.location.href='/#'
      }
      
      this.segu = await request.json();
      // console.log(request.ok);
      
      
    },
    
    

  },

  mounted() {
    if (window.localStorage) {
    if (window.localStorage.getItem('token') !== undefined
      && window.localStorage.getItem('token')
    ){

    }else{
      window.location.href='/#'
    }
  }else{
      window.location.href='/#'
    }
    this.llenaMascotas();
    
    this.buscar(localStorage.Id);
  },
  
};



</script>
  
<style>
</style>