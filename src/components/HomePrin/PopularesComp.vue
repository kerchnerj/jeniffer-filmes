<script>
import CardFilmesSection3 from "../Cards/CardFilmesSection3.vue";
import FilmeApi from "../../api/filmes.js";
const filmeapi = new FilmeApi();
export default {
  components: {
    CardFilmesSection3
  },
  data() {
    return {
      filmes: [],
    };
  },
  async created() {
    this.filmes = await filmeapi.BuscarTodosPopulares();
  },
  methods: {
    getPosterUrl(poster_path) {
      return `https://image.tmdb.org/t/p/w500${poster_path}`;
    },
  },
};
</script>

<template>
    <div class="section32">
    <div>
      <div>
        <h3 class="PoEmh3"><b>Populares</b></h3>
        <div class="filmes-linhas">
          <CardFilmesSection3
            v-for="filme of filmes"
            :key="filme.id"
            :link_filme="filme"
            :poster="getPosterUrl(filme.poster_path)"
            :nome_fsa="filme.title"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.section32 {
  background-color: white;
  margin: 10px;
  color: black;
  display: flex;
  margin-left: 16px;
  margin-top: 10px;
  border-radius: 20px;
}
.PoEmh3{
  font-size: 2.5em;
  margin-left: 22px;
}
#section3-container{
  width: 21%;
}
.filmes-linhas {
  display: flex;
  justify-content: center;
}
</style>