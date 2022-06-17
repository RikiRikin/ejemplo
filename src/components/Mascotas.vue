

<script >

export default {
  name: "Mascotas",

  data() {
    return {
      
      segundamascotas: [],
      error: [],
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
   async eliminar(id){
      // axios.get("http://localhost:8080/Mascotas/"+id).then((result) => {
       
      // })
      // this.llenaMascotas();
    if(!confirm('¿Deseas eliminar?')){
        return;
    }

    const request = await fetch('http://localhost:8080/api/mascotas/'+ id, {
            method: 'DELETE',
            headers: {'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': localStorage.token},
          });

this.llenaMascotas();
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
      
      this.segundamascotas = await request.json();
      // console.log(request.ok);
      
      
    },

    guardarId(id){
      if(localStorage.Id){
        localStorage.removeItem("Id")
      }
      localStorage.Id = id;
    }
  },

  mounted() {
    if (window.localStorage) {
    if (window.localStorage.getItem('token') !== undefined
      && window.localStorage.getItem('token')
    ){
this.navStatus = false
    }else{
      window.location.href='/#'
    }
  }else{
      window.location.href='/#'
    }
    this.llenaMascotas();
    
    
    
  },
};



</script>
  
<style>
</style>

<template>
  
  <section>
    
    <div class="container mt-4">
      <h3>Mascotas</h3> <br>
      
      <div class="card" >
        <div class="card-body">
          <h4 class="card-title">
            <a name="" id="" href="http://localhost:8081/#/Mascotas/registrar" class="btn btn-primary" role="button" > Nuevo</a>
            <hr>
            <table class="table table-success table-striped">
              <thead>
                <tr>
                  <th scope="col">Id</th>
                  <th scope="col">Nombre</th>
                  <th scope="col">Edad</th>
                  <th scope="col">Raza</th>
                  <th scope="col">Opciones</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="cota in segundamascotas" :key="cota.id">

                  <th scope="row">{{ cota.id }}</th>
                  <td>{{ cota.nombre }}</td>
                  <td>{{ cota.raza }}</td>
                  <td>{{ cota.edad }}</td>
                  <td>
                    <div class="d-flex justify-content-evenly bd-highlight">
                      <a type="button" class="btn btn-primary" href="http://localhost:8081/#/Mascotas/modificar" @click="guardarId(cota.id)" >
                        <i class="bi bi-pencil-square" ></i>
                      </a>
                      <button type="button" class="btn btn-danger" @click="eliminar(cota.id)" id="buttonDeleteConfir">
                        <i class="bi bi-trash"></i>
                      </button>
                    </div>

                  </td>
                </tr>

              </tbody>
            </table>
          </h4>
        </div>
      </div>
    </div>
  </section>
</template>