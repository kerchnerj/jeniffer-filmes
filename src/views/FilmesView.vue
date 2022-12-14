<script>
import axios from "axios";
import CardFilmesComp from "../components/cards/CardFilmesComp.vue";
import FiltroCompFilme from "../components/filtros/filtroCompFilme.vue";
import FilmeApi from "../api/filmes.js";
import FiltrosApi from "../api/filtros.js";
const filtrosapi = new FiltrosApi();
const filmeapi = new FilmeApi();
export default {
  components: { CardFilmesComp, FiltroCompFilme },
  data() {
    return {
      filmes: [],
      generos: [],
    };
  },
  async created() {
    this.filmes = await filmeapi.BuscarTodosOsFilmes();
    this.generos = await filtrosapi.buscarTodosOsGenerosFilme();
  },
  methods: {
    getPosterUrl(poster_path) {
      return `https://image.tmdb.org/t/p/w500${poster_path}`;
    },
    async buscar(params) {
      if (params.genero !== "") {
        this.filmes = await filmeapi.BuscarFilmesPorGenero(params.genero);
      } else if (params.filme === "") {
        this.filmes = await filmeapi.BuscarTodosOsFilmes();
      } else {
        const url = `https://api.themoviedb.org/3/search/movie?api_key=4f2d6721f9937522fb8b76dbac0eab07&language=pt-BR&query=${params.filme}&page=1&include_adult=false`;
        const { data } = await axios.get(url);
        this.filmes = data.results;
      }
    },
  },
};
</script>
<template>
  <div>
    <div class="dentro">
      <FiltroCompFilme @buscar="buscar" />
      <div class="todos-filmes">
        <CardFilmesComp
        v-for="filme of filmes"
        :nome_fsa="filme.title"
        :key="filme.id"
        :link_filme="filme"
        :poster="getPosterUrl(filme.poster_path)"
        />
      </div>
    </div>
  </div>
</template>
