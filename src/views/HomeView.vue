<script>
import EmCartazComp from "../components/HomePrin/EmCartazComp.vue";
import PopularesComp from"../components/HomePrin/PopularesComp.vue";
import PEstreiasComp from "../components/HomePrin/PEstreiasComp.vue";
import MaisAvaliadosComp from "../components/HomePrin/MaisAvaliadosComp.vue";
export default {
  components: {
    PopularesComp,
    EmCartazComp,
    PEstreiasComp,
    MaisAvaliadosComp
}
}
</script>
<template>
  <div class="LandingPage">
      <section class="tghb-section">
        <h2>MoviesFlix</h2>
        <p>
          Filmes, trailers, horários e salas de cinema, notícias, críticas o site
          de <strong>Cinema nº1 do Brasil!</strong> As últimas notícias do cinema, trailers e
          entrevistas, horários de filmes, o mais completo banco de dados sobre
          cinema
        </p>
      </section>
    </div>
      <EmCartazComp />
      <PopularesComp />
      <PEstreiasComp />
      <MaisAvaliadosComp />
</template>

<style></style>
