<template>

  <section class="src-componentes-formulario">
    <vue-form :state="formState" @submit.prevent="enviar()">
      
      <!--CAMPO Y VALIDACIONES-->

      <validate tag="div">
        <label for="nombre">Nombre</label>
        <input
          type="text"
          id="nombre"
          class="form-control"
          name="nombre" 
          autocomplete="off"
          v-model.trim="formData.nombre"
          required 
          :minlength="minNombre"
          :maxlength="maxNombre"
          no-espacios
        />
  
        <field-messages name="nombre" show="$dirty">
          <div slot="required"    class="alert alert-danger mt-1"> Campo requerido</div>
          <div slot="minlength"   class="alert alert-danger mt-1"> Minimo {{minNombre}} caracteres</div>
          <div slot="no-espacios" class="alert alert-danger mt-1"> No se pueden colocar espacios intermedios </div>
        </field-messages>
      </validate>

      <br>

      <!--CAMPO Y VALIDACIONES-->

      <validate tag="div">
        <label for="edad">Edad</label>
        <input
          type="number"
          id="edad"
          class="form-control"
          name="edad" 
          autocomplete="off"
          v-model.number="formData.edad"
          required
          :min="edadMin"
          :max="edadMax"
        />
  
        <field-messages name="edad" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          <div slot="min"      class="alert alert-danger mt-1">Edad mínima {{edadMin}}</div>
          <div slot="max"      class="alert alert-danger mt-1">Edad fuera de rango {{edadMax}}</div>
        </field-messages>
      </validate>

      <br>

      <!--CAMPO Y VALIDACIONES-->

      <validate tag="div">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          class="form-control"
          name="email" 
          autocomplete="off"
          v-model="formData.email"
          required 
        />
  
        <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
        </field-messages>
      </validate>

      <br>
  
      <button class="btn btn-success my-3" :disabled="formState.$invalid">ENVIAR</button>
    </vue-form>

    <br>
    <label><h2>Tabla de Usuarios</h2></label>
    <br>

    <div v-if="usuarios.length" class="table-responsive">
      <table class="table">
        <tr>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Email</th>
        </tr>
        <tr v-for="(usuarioRecorrido, index) in usuarios" :key="index">
          <td>{{  usuarioRecorrido.nombre  }}</td>
          <td>{{  usuarioRecorrido.edad    }}</td>
          <td>{{  usuarioRecorrido.email    }}</td>
        </tr>
      </table>
    </div>
    <h3 v-else class="alert alert-danger"> No se han ingresado datos.</h3>

  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState: {

        },
        formData: this.getInitialData(),
        usuarios: [],
        edadMin: 18,
        edadMax: 120,
        minNombre: 5,
        maxNombre: 15,

      }
    },
    methods: {
      getInitialData(){
        return {
          nombre:   null,
          apellido: null,
          edad:     null,
          email:    null,
        }
      },
      enviar(){
        let usuarioIngresado = {...this.formData}
        console.log(usuarioIngresado)
        this.usuarios.push(usuarioIngresado)

        this.formData = this.getInitialData()
        this.formState._reset()
      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">


</style>
