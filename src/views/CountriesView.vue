<script>
import countries from "/src/datasets/countries.json";
import CountryComponent from "../components/CountryComponent.vue";

export default {
  name: "CountriesView",
  components: {
    CountryComponent,
  },
  data() {
    return {
      countries: [],
      paisActual: "",
    };
  },
  created() {
    this.countries = countries;
  },
  methods: {
    filtrar(e) {
      // : Implementar. filtra el país de acuerdo al valor del input. Hint: Recuerda la función filter
      this.filtro = e.target.value;
    },
    filtrarPais() {
      // : Implementar. filtra el país de acuerdo al valor del input. Hint: Recuerda la función filter
      this.countries = countries.filter((country) => {
        return country.name.toLowerCase().includes(this.filtro.toLowerCase());
      });

    },
  },
};



</script>

<template>
  <div class="countries">
    <input
      placeholder="Busca un país"
      :value="this.paisActual"
      @input="filtrar"
    /> 
    <button @click="filtrarPais">Buscar</button>
  </div>
  <div class="countries-container">
    <!--//: pasar una propiedad para determinar si al componente se le puede hacer click-->
    <!--//la propiedad debe llamarse "clickable" y debe ser booleana-->

    <CountryComponent
      v-for="(country, index) in countries"
      :key="index"
      :name="country.name"
      :capital="country.capital"
      :currency_name="country.currency_name"
      :currency="country.currency"
      :region="country.region"
      :code="country.iso2"
      :image="country.image"
      :clickable="false" 
    ></CountryComponent>
  </div>
</template>

<style scoped>
@media (min-width: 1024px) {
  .countries {
    align-items: center;
    justify-content: center
  }

    input {
      width: 50%;
      height: 30px;
      border-radius: 5px;
      border-color: grey;
      border-style: solid;
      margin: 10px;
      line-height: 2em;
    }


  .countries-container {
    display: grid;
    grid-template-columns: auto auto auto;
    grid-gap: 10px;
    align-items: center;
    overflow-y: auto;
    vertical-align: middle;
    
    
  }
}
</style>

