<script>
import axios from "axios";
import CardSeriesComp from "../components/Cards/CardSeriesComp.vue";
import filtroCompSerie from "../components/filtros/filtroCompSerie.vue";
import SeriesApi from "../api/series.js";
import FiltrosApi from "../api/filtros.js";
const filtrosapi = new FiltrosApi();
const seriesapi = new SeriesApi();
export default {
  components: { CardSeriesComp, filtroCompSerie },
  data() {
    return {
      series: [],
      generos: [],
    };
  },
  async created() {
    this.series = await seriesapi.BuscarTodasAsSeries();
    this.generos = await seriesapi.BuscarSeriesPorGenero();
  },
  methods: {
    getPosterUrl(poster_path) {
      return `https://image.tmdb.org/t/p/w500${poster_path}`;
    },
    async buscar(params) {
      if (params.genero !== "") {
        this.series = await filtrosapi.BuscarSeriesPorGenero(params.genero);
      } else if (params.serie === "") {
        this.series = await seriesapi.BuscarTodasAsSeries();
      } else {
        const url = `https://api.themoviedb.org/3/search/tv?api_key=4f2d6721f9937522fb8b76dbac0eab07&language=pt-BR&query=${params.serie}&page=1&include_adult=false`;
        const { data } = await axios.get(url);
        this.series = data.results;
      }
    },
  },
};
</script>
<template>
  <div>
    <div class="dentro">
      <filtroCompSerie @buscar="buscar"/>
      <div class="todos-filmes">
        <CardSeriesComp
        v-for="serie of series"
        :nome_fsa="serie.name"
        :key="serie.id"
        :link_serie="serie"
        :poster="getPosterUrl(serie.poster_path)"
        />
      </div>
    </div>
  </div>
</template>

<style>
.dentro {
  margin: 20px;
  background-color: white;
  border-radius: 15px;
}
</style>
