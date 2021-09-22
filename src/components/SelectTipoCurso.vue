<template>

<select class="form-control" name="idTipoCursoFK" id="idTipoCursoFK">
    <option v-for="tipoCurso in ListaTipoCurso" :key="tipoCurso.idTipoCurso"
     :value="tipoCurso.idTipoCurso">{{tipoCurso.nombreTipoCurso}}
     </option>
</select>

</template>

<script>
import axios from 'axios';


export default {
    name:"SelectTipoCurso",
   data(){
        return {
            ListaTipoCurso:null,
        }
        
    },
    mounted:function(){
        let direccion = "http://localhost:5000/api/TipoCurso/";
                axios.get(direccion).then( data =>{
                this.ListaTipoCurso = data.data;
                  }); 
    }
    
        
}

</script>
