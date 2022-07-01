<template>

  <section class="src-componentes-tabla">
    <div class="jumbotron">
      <label><h2>Tabla de Usuarios MockApi</h2></label>
      <hr>
      <hr>
      <br>

      <button class="btn btn-warning my-3 mr-3" @click="getUsuariosXHRcb()">Pedir XHR  </button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosFetch()">Pedir Fetch</button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Pedir Axios</button>
      <button class="btn btn-danger my-3 mr-3" @click="usuarios = []">Clear</button>
      <br>

      <div v-if="usuarios.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(usuarioRecorrido, index) in usuarios" :key="index">
            <td>{{  usuarioRecorrido.nombre      }}</td>
            <td>{{  usuarioRecorrido.email       }}</td>
            <td>{{  usuarioRecorrido.telefono    }}</td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-danger"> No se han ingresado datos.</h3>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-tabla',
    props: [],
    mounted () {

    },
    data () {
      return {
        url: 'https://6286f9227864d2883e7c4e53.mockapi.io/usuarios/',
        usuarios: [],
      }
    },
    methods: {
      getUsuariosXHRcb() {
        const xhr = new XMLHttpRequest()
        xhr.open('get',this.url)
        
        xhr.addEventListener('load', () => {
          try{
            let respuesta = JSON.parse(xhr.response)
            this.usuarios = respuesta
          }
          catch(error) {
            console.error('Error en XHR status:', xhr.status)
          }
        })
        xhr.send()

      },
      async getUsuariosFetch() {
        try {
          let response = await fetch(this.url)
          let respuesta = await response.json()
          this.usuarios = respuesta
        }
        catch(error) {
          console.error('Error en Fetch:', error)
        }
      },
      async getUsuariosAxios(){
        try{
          let {data:usuarios} = await this.axios(this.url)
          this.usuarios = usuarios
        }catch(error){
          console.error('Error en Axios', error.message)
        }

      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron{
    background-color: blueviolet;
  }
  .table-responsive{
    background-color: white;
  }
  label{
    color: white
  }
</style>
