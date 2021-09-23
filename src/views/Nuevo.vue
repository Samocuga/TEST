<template>
<div>
    <center>
        <v-form ref="form">
            <legend>Creacion Anuncio</legend>
            <div  >
                <v-textarea v-model="form.mensajeAnuncio" :counter="500" label="Name" required></v-textarea>
            </div>
            <div>
              <v-text-field type="date" v-model="form.fechaInicio" label="Fecha Inicio" required></v-text-field>
            </div>
            <div>
              <v-text-field type="date" v-model="form.fechaFinal" label="Fecha Final" required></v-text-field>
            </div>
            <div>
                <v-btn color="blue" v-on:click="guardar()">Crear</v-btn>
                <v-btn color="warning" v-on:click="salir()" >Salir</v-btn>
            </div> 
        </v-form>
    </center>
</div>
</template>
<script>
//import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return {
            form:{
                "estadoAnuncio": "",
                "mensajeAnuncio": "",
                "fechaInicio": "",
                "fechaFinal": "",
                "idUsuarioFK":"",
        },
        }
    },
    components:{
        //Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.idUsuarioFK = document.getElementById("idUsuarioFK").value       
            axios.post("http://localhost:3000/api/Anuncio",this.form)
         .then(data =>{
                    console.log(data);
                 this.$router.push("/dashboard"); 
            })
        },
        salir(){
            this.$router.push("/dashboard");
        }, 
    }
}
</script>