<template>

<select v-model"form.idUsuarioFK"  name="idUsuarioFK" id="idUsuarioFK">
    <option v-for="Usuario in ListaUsuario" :key="Usuario.idUsuario"
     >{{Usuario.nombreUsuario}} {{Usuario.apellidoUsuario}}
     </option>
</select>
</template>

<script>
import axios from 'axios';


export default {
    name:"SelectUsuario",
   data() {
        return {
            ListaUsuario:null,
        }
   },
    mounted:function(){
        let direccion = "http://localhost:3000/api/usuarios";
                axios.get(direccion).then( data =>{
                this.ListaUsuario = data.data;
                  });
    }
}
</script>