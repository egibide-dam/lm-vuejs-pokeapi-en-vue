<template>
  <nav class="row navbar navbar-expand p-4 text-bg-secondary">
    <div class="container-fluid">
      <h1>
        <RouterLink class="nav-link text-bg-secondary" :to="{ name: 'home' }">PokéAPI en Vue</RouterLink>
      </h1>
      <div class="collapse navbar-collapse">
        <ul class="navbar-nav m-0 align-items-center ms-auto">
          <li class="nav-item">
            <RouterLink class="nav-link text-bg-secondary" :to="{ name: 'home' }">Home</RouterLink>
          </li>
          <li class="nav-item mx-2">|</li>
          <li class="nav-item">
            <RouterLink class="nav-link text-bg-secondary" :to="{ name: 'pokemon' }">Pokémon</RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  name: 'BarraNavegacion'
}
</script>