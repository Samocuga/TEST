<template>

<select class="form-control" name="idRequisitosFK" id="idRequisitosFK">
    <option v-for="tipoRequisito in ListatipoRequisito" :key="tipoRequisito.idRequisitos"
     :value="tipoRequisito.idRequisitos">{{tipoRequisito.nombreRequisitos}}
     </option>
</select>

</template>

<script>
import axios from 'axios';


export default {
    name:"SelectRequisito",
   data(){
        return {
            ListatipoRequisito:null,
        }
        
    },
    mounted:function(){
        let direccion = "http://localhost:5000/api/Requisito/";
                axios.get(direccion).then( data =>{
                this.ListatipoRequisito = data.data;
                  }); 
    }
    
        
}

</script>