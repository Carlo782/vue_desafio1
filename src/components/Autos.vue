<template>
<div v-for="auto in autos" :key="auto.index">
  {{ auto }}



</div>


</template>

<script>
import axios from 'axios'

export default{
    name:'Autos_A',
    data(){
        return{
            autos:[],
            

        }
    },


    mounted(){
        let vue=this;
        axios.get("http://localhost:8080/automoviles/listar").then(function(response){
            vue.autos=response.data;
            console.log(vue.autos)


        })
    },
    methods:{
     

    },

}

</script>