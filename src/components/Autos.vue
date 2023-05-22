<template>
  <div>
    <div>

      <form @submit.prevent="formFiltrar">
       <input type="number" v-model="precio">
        <select v-model="opcion">
          <option value="">Tipo de filtro</option>
          <option value="Mayor">Mayor</option>
          <option value="Menor">Menor</option>
        </select>
        <button class="btn btn-outline-secondary" type="submit">Filtrar</button>
      </form>


      <form @submit.prevent="formGenerar">
        <input type="number" v-model="cantidad">
        <button class="btn btn-outline-secondary" type="submit">Generar Auto/s</button>
      </form>

    </div>
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
          <th scope="col">Popularidad</th>
          <th scope="col">Cabinas</th>
          <th scope="col">Sunroof</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="auto in autos" :key="auto.id">
          <td>{{ auto.id }}</td>
          <td>{{ auto.marca }}</td>
          <td>{{ auto.anio }}</td>
          <td>{{ auto.color }}</td>
          <td>{{ auto.precio }}</td>
          <td>{{ auto.turbo }}</td>
          <td>{{ auto.tipo }}</td>
          <td>{{ auto.motor }}</td>
          <td>{{ auto.popularidad }}</td>
          <td>{{ auto.cabinas }}</td>
          <td>{{ auto.sunroof }}</td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Autos_A',
  data() {
    return {
      autos: [],
      cantidad: 0,
      precio: 0,
      opcion: "",
    }
  },

  created() {
    this.vistaInicial();


  },

  methods: {

    vistaInicial() {
      axios.get(`http://localhost:8080/automoviles/listar`)
        .then(response => {
          this.autos = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },

    generarFiltroPreciosSelect() {
      axios.get(`http://localhost:8080/automoviles/listar`)
        .then(response => {
          this.autos = response.data;
        })  
    },

    generar() {
      axios.get(`http://localhost:8080/automoviles/generar?cantidad=${(this.cantidad - 1)}`)
        .then(response => {
          this.autos = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },

    mostrarFiltradoPrecio() {

      if (this.opcion === "Mayor") {
        axios.get(`http://localhost:8080/automoviles/filtrar/mayores?precio=${(this.precio)}`)
          .then(response => {
            this.autos = response.data;
          })
          .catch(error => {
            console.error(error);
          });

      } else if (this.opcion === "Menor") {

        axios.get(`http://localhost:8080/automoviles/filtrar/menores?precio=${(this.precio)}`)
          .then(response => {
            this.autos = response.data;
          })
          .catch(error => {
            console.error(error);
          });

      } else {
        this.vistaInicial();
      }

    },

    formGenerar() {
      this.generar();
    },

    formFiltrar() {
      this.mostrarFiltradoPrecio();
    }


  }

}
</script>