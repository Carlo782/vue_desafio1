<template>
<div>
    <form @submit.prevent="submitForm">
        <input type="number" v-model="cantidad">
        <button type="submit">Generar</button>
    </form>
    <table class="table table-striped" v-if="autos">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Brand</th>
          <th scope="col">Year</th>
          <th scope="col">Color</th>
          <th scope="col">Price</th>
          <th scope="col">Turbo</th>
          <th scope="col">Type</th>
          <th scope="col">Motor</th>
          <th scope="col">Popularity</th>
          <th scope="col">Cabinas</th>
          <th scope="col">Sunroof</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="auto in autos" :key="auto.id">
          <td>{{auto.id}}</td>
          <td>{{auto.marca}}</td>
          <td>{{auto.anio}}</td>
          <td>{{auto.color}}</td>
          <td>{{auto.precio}}</td>
          <td>{{auto.turbo}}</td>
          <td>{{auto.tipo}}</td>
          <td>{{auto.motor}}</td>
          <td>{{auto.cabinas}}</td>
          <td>{{auto.sunroof}}</td>
        </tr>
      </tbody>
    </table>

</div>


</template>

<script>
import axios from 'axios'

export default{
    name:'Autos_A',
    data(){
        return{
            autos:[],
            cantidad:0,
            

        }
    },
    
    methods:{
    generar(){
      axios.get("http://localhost:8080/automoviles/generar?cantidad=${this.cantidad}")
        .then(response => {
          this.autos = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    submitForm(){
      this.generar();
    }
  }

}

</script>