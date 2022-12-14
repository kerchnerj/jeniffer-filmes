<script>
import axios from "axios";
import SeriesApi from "../../api/series.js";
const seriesapi = new SeriesApi();
export default {
  data() {
    return {
      name: {},
      serie: "",
    };
  },
  components: {},
  props: {
    poster: String,
    nome_serie: String,
    serie_id: Number,
    sinopse_serie: String,
    duracao: Number,
  },
  async created() {
    this.series = await seriesapi.BuscarTodasAsSeries();
    const url = `https://api.themoviedb.org/3/tv/${this.id}?api_key=4f2d6721f9937522fb8b76dbac0eab07&language=pt-BR`;
    const { data } = await axios.get(url);
    this.serie = data;
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
        <h2 class="Tit_Filme">{{ nome_serie }}</h2>
        <p class="Desc_Filme">{{ sinopse_serie }}</p>
      </div>
    </div>
  </div>
</template>
