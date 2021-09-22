<template>
    <div>
        <v-btn color="success" v-on:click="nuevo()">Nuevo Anuncio</v-btn>
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
                  MENSAJE
                </th>
                <th class="primary--text">
                  FECHA INICIO
                </th>
                <th class="primary--text">
                  FECHA FINAL
                </th>
                <th class="primary--text">
                  CREADOR
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="Anuncio in Anuncios" :key="Anuncio.idAnuncio" v-on:click="editar(Anuncio.idAnuncio)">
                        <td>{{Anuncio.idAnuncio}}</td>
                        <td>{{Anuncio.estadoAnuncio}}</td>
                        <td>{{Anuncio.mensajeAnuncio}}</td>
                        <td>{{Anuncio.fechaInicio}}</td>
                        <td>{{Anuncio.fechaFinal}}</td>
                        <td>{{Anuncio.Usuario.nombreUsuario}}</td>
                    </tr>
            </tbody>
          </v-simple-table>
      </div>
</template>
<script>
//import Header from '@/components/Header.vue'
import axios from 'axios'
export default {
    name:"Dashboard",
    data(){
        return {
            Anuncios:null,
            pagina:1
        }
    },
    components:{
        //Header
    },
     methods:{
       consultarInactivos(){
                 let direccion = "http://localhost:3000/api/Anuncio/inactivos";
                axios.get(direccion).then( data =>{
                    this.anuncio = data.data;
                    console.log(this.anuncio)
                }); 
            },
            editar(id){
                this.$router.push('/editar/' + id);
                console.log(id)
            },
            nuevo(){
                this.$router.push('/nuevo');
            }
            
    },
      mounted:function(){
        let direccion = "http://localhost:3000/api/Anuncio";
        axios.get(direccion).then( data =>{
            this.Anuncios = data.data;
            console.log(this.Anuncios)
        });
    },
        
}
</script>
<style lang="stylus" scoped>

</style>