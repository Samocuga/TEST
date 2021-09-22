<template>
 <div>
             <Header/>
    <div >
<form >
     <div>
         <label for="">Curso</label>
            <div>
                <SelectCurso />
                
            </div>
            <div>
            <SelectUsuario/>
              </div>  
        </div>
        <button type="button"  v-on:click="salir()" >Salir</button>
        <button type="button"  v-on:click="guardar()" >Guardar</button>
</form>
    </div>
    
    <Footer/>
 </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import SelectCurso from '@/components/SelectCurso.vue';
import SelectUsuario from '@/components/SelectUsuario.vue';
import axios from 'axios';

export default {
    
    name:"InscripcionN",
    data() {
        return{  
            form:{
                 'idCursoFK': '',
            }
        }
    },
    components:{
        Header ,
        Footer,
         SelectCurso,
         SelectUsuario
    },
    methods:{
        guardar(){/* 
            this.form.token = localStorage.getItem("token"); */
            axios.post("http://localhost:3000/api/InscripcionRoute",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Anuncio creado","success");
                this.salir();
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/Inscripcion");
        },
        cambiarCurso(tipo){
            this.form.idCursoFK = tipo
        },
        
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
        
    }
}

</script>
<style scoped>

</style>