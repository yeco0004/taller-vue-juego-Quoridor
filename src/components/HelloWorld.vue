<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="hello-world">
    <h1 class="hello-world__title">{{ msg }}</h1>
    <h3 class="hello-world__subtitle">
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
  </div>
</template>

<style scoped>
.hello-world__title {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

.hello-world__subtitle {
  font-size: 1.2rem;
}

.hello-world__title,
.hello-world__subtitle {
  text-align: center;
}

@media (min-width: 1024px) {
  .hello-world__title,
  .hello-world__subtitle {
    text-align: left;
  }
}
</style>
