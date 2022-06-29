<template >

 <div class="jumbotron">
  <button class="btn btn-success my-3 mr-3" @click="getUsuariosXHRcb()" > Pedir XHR</button>
  <button class="btn btn-success my-3 mr-3" @click="getUsuariosFetch()" > Pedir Fetch</button>
  <button class="btn btn-danger my-3 mr-3" @click="usuarios=[]" > Borrar</button>

    <div class="table-responsive">
      <table class="table table-dark">
          <tr>
              <th>id</th>
              <th>nombre</th>
              <th>edad</th>
              <th>email</th>
          </tr>
          <tr v-for="(usuario,index) in usuarios" :key="index">
              <td>{{ index + 1 }}</td>
              <td>{{ usuario.nombre }}</td>
              <td>{{ usuario.email }}</td>
              <td>{{ usuario.nrotel }}</td>
              
          </tr>
      </table>

</div>
 </div>
</template>

<script lang="js">

  export default  {
    name: 'src-componentes-tabla-personas',
    props: [],
    mounted () {

    },
    data () {
      return {
        url:'https://6286bd1ee9494df61b2cbd05.mockapi.io/tp2/usuarios/usuarios' ,
        usuarios: [],
      }
    },
    methods: {
      getUsuariosXHRcb(){
            const xhr= new XMLHttpRequest()
            xhr.open('get',this.url)
            xhr.addEventListener('load',() =>{
              let respuesta = JSON.parse(xhr.response)
              console.log(typeof respuesta,respuesta )
              this.usuarios=respuesta
            })
            xhr.send()
        },
       async getUsuariosFetch(){
           try{
            let response = await fetch(this.url) //pongo await cuando quiero esperar que una promesa se cumpla
            let respuesta= await response.json()
              console.log(respuesta)
              this.usuarios=respuesta
            }
            catch( error){
              console.error('Error en Fetch:', error)
            }
        }
        },
    
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-tabla-personas {


  }
  jumbotron{
    background-color:darkolivegreen ;
    color:rgb(231, 203, 168) ;
  }
</style>
