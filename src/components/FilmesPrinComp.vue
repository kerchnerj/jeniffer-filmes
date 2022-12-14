<script>
import axios from "axios";
import FilmeApi from "../api/filmes.js";
const filmeapi = new FilmeApi();
export default {
    data() {
        return {
            name: {},
        };
    },
    components: {},
    props: {
        poster: String,
        nome_filme: String,
        sinopse_filme: String,
    },
    async created() {
        this.filmes = await filmeapi.BuscarTodosOsFilmes();
        const url = `https://api.themoviedb.org/3/movie/${this.id}/credits?api_key=df0a1976ab5aa969146a8dbff08f0123&language=pt-BR`;
        const { data } = await axios.get(url);
    },
    methods: {
        getPosterUrl(profile_path) {
            return `https://image.tmdb.org/t/p/w500${profile_path}`;
        },
    },
};
</script>

<template>
  <div class="lds">
    <div class="all-t">
      <img class="Img_Filme" :src="poster" alt="">
      <div class="paids">  
        <h2 class="Tit_Filme">{{ nome_filme }}</h2>
        <p class="Desc_Filme">{{ sinopse_filme }}</p>
      </div>
    </div>
  </div>
</template>

<style>
.paids {
  flex-direction: column;
  margin-left: 50px;
}

.all-t {
  display: flex;
}

.lds{
  margin-left: 2%;
  margin: 15px;
  background-color: white;
  padding: 20px;
}
/*--------------------------------------------------*/
.Img_Filme {
  height: 80vh;
  width: auto;
}

.Tit_Filme{
  font-size: 40px;
  color: rgb(0, 0, 0);
  margin-top: 20px;
}

.Desc_Filme{
  max-width: 900px;
  margin-right: 500px;
  font-size: 1.5em;
}
</style>