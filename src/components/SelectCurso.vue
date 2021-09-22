<template>

<select class="form-control" name="idCursoFK" id="idCursoFK">
    <option v-for="Curso in ListaCurso" :key="Curso.idCurso"
     :value="Curso.idCurso">{{Curso.nombreCurso}}
     </option>
</select>

</template>

<script>
import axios from 'axios';


export default {
    name:"SelectCurso",
   data(){
        return {
            ListaCurso:null,
        }
        
    },
    mounted:function(){
        let direccion = "http://localhost:5000/api/Curso/";
                axios.get(direccion).then( data =>{
                this.ListaCurso = data.data;
                  }); 
    }
    
        
}

</script>