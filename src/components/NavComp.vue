<script>
export default {};
</script>
<template>
  <nav>
    <div class="logo">
      <router-link to="/" style="text-decoration: none;">MoviesFlix</router-link>
    </div>
    <ul>
      <li>
        <router-link class="filmes-link" to="/filmes" style="text-decoration: none;">Filmes</router-link>
      </li>
      <li>
        <router-link class="series-link" to="/series" style="text-decoration: none;">Series </router-link>
      </li>
    </ul>
  </nav>
</template>
