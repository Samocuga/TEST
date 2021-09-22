<template>
<div>
    <Header/>
<div >
    <center>
        <v-form>
            
            <!-- Form Name -->
            <legend>Edicion Anuncio</legend>
            
           <div>
                <v-textarea v-model="form.mensajeAnuncio" :counter="500" label="Name" required></v-textarea>
            </div>
            
            <!-- Text input-->
            <div  >
              <v-text-field type="date" v-model="form.fechaInicio" label="Fecha Inicio" required></v-text-field>
            </div>
            <!-- Text input-->
            <div  >
              <v-text-field type="date" v-model="form.fechaFinal" label="Fecha Final" required></v-text-field>
            </div>
            <!-- Button -->
            <div >
              <v-btn color="blue" v-on:click="editar()">Editar</v-btn>
              <v-btn color="warning" v-on:click="salir()" >Salir</v-btn>
              <v-btn  v-on:click="functionBtn(botonForm.valor, botonForm.idAnuncio)" >{{botonForm.valor}}</v-btn>
            </div> 
            </v-form>
          </center>
    </div>
</div>
</template>

<script>
import Header from '@/components/Header.vue';
import axios from 'axios';
export default {
  name:"Editar",
  components:{
    Header,
    //Footer
  },
  data:function(){
    return {
        form:{
                "idAnuncio":"",
                "estadoAnuncio": "",
                "mensajeAnuncio": "",
                "fechaInicio": "",
                "fechaFinal": "",
                "UsuarioFK":""
        },
        botonForm:{
          "valor":"",
          "idAnuncio":"",
          
        }
    }
  },
  methods:{
      salir(){
        this.$router.push("/dashboard");
      },
      editar(){
          axios.put("http://localhost:3000/api/Anuncio/actualizar/"+this.form.idAnuncio, this.form)
          .then( data =>{
              console.log(data);
              this.salir();
          })
      },
      functionBtn(accion, idAnuncio){
            axios.put("http://localhost:3000/api/Anuncio/"+accion+"/"+idAnuncio)
              .then( data =>{
                  console.log(data);
                  this.salir();
              })
          }
  },
  mounted:function(){
      this.form.idAnuncio = this.$route.params.id;
      axios.get("http://localhost:3000/api/Anuncio/id/"+ this.form.idAnuncio)
      .then( datos => {
        console.log(datos)
        this.form.estadoAnuncio = datos.data.estadoAnuncio;
        this.form.mensajeAnuncio = datos.data.mensajeAnuncio;
        this.form.fechaInicio = datos.data.fechaInicio;
        this.form.fechaFinal = datos.data.fechaFinal;

        this.botonForm.idAnuncio = this.form.idAnuncio;

         let estado = datos.data.estadoAnuncio;
        if(estado == "Activo"){
          this.botonForm.valor = "Inhabilitar"
        }else{
          this.botonForm.valor = "Activo"
        }

        console.log(this.form);
      })
  },
}

    
</script>