<template>
  <div class="home">
      <h1>Github Slam Attax Card</h1>
      <h2>Make your own</h2>

      <slot></slot>
  </div>
</template>

<script>
export default {
    name: 'HomeTemplate'
}
</script>

<style>

.home {
    background: rgb(22, 22, 22);
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-content: center;
    align-items: center;
}

</style>