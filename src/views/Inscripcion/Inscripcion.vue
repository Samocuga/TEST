<template>
    <div>
        <v-btn color="success" v-on:click="nuevo()">Nueva Inscripcion</v-btn>
        <v-btn color="orange" text  v-on:click="consultarInactivos()" >Cursos Inactivos</v-btn>

          <v-simple-table>
            <thead>
              <tr>
                <th class="primary--text">
                  ID
                </th>
                <th class="primary--text">
                  ESTADO
                </th>
                <th class="primary--text">
                  CURSO
                </th>
                <th class="primary--text">
                  INSCRITO
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="Inscripcion in Inscripciones" :key="Inscripcion.idInscripcion" v-on:click="editar(Inscripcion.idInscripcion)">
                        <td>{{Inscripcion.idInscripcion}}</td>
                        <td>{{Inscripcion.estadoInscripcion}}</td>
                        <td>{{Inscripcion.Curso.nombreCurso}}</td>
                        <td>{{Inscripcion.Usuario.nombreUsuario}} {{Inscripcion.Usuario.apellidoUsuario}}</td>
                    </tr>
            </tbody>
          </v-simple-table>
      </div>
</template>

<script>
import axios from 'axios';
export default {
    name:"Inscripcion",
    data(){
        return{
            Inscripciones:null,
              botonForm:{
          "valor":"",
          "idInscripcion":"",
          
        }
        }
    },
    components:{
       /* Header,
         Footer */
    },
    methods:{
            consultarInactivos(){
                 let direccion = "http://localhost:3000/api/InscripcionRoute/inhabilitar";
                axios.get(direccion).then( data =>{
                    this.Inscripcion= data.data;
                    console.log(this.Inscripcion)
                }); 
            },
        editar(id){
            this.$router.push('/EditarIns/'+id);
        },
        nuevo(){
           this.$router.push('/InscripcionN');
        }
    },
    functionBtn(accion, idInscripcion){
            axios.put("http://localhost:3000/api/InscripcionRoute/"+accion+"/"+idInscripcion)
              .then( data =>{
                  console.log(data);
                  this.salir();
              })
          },
    mounted:function(){
        let url = "http://localhost:3000/api/InscripcionRoute/";
        axios.get(url).then(data => {
         console.log(data)
            this.Inscripciones= data.data;
            this.botonForm.idInscripcion = this.idInscripcion;

             let estado = data.data.estadoInscripcion;
        if(estado == "Activo"){
          this.botonForm.valor = "inhabilitar"
        }else{
          this.botonForm.valor = "Activar"
        }          
            console.log(this.Inscripciones)
        })

    }
}
</script>

<style scoped>

</style>