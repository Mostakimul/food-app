<template>
  <main class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants</h1>
    </div>
    <TheResturantInfo />
  </main>
</template>

<script>
import TheResturantInfo from '@/components/TheResturantInfo.vue'

export default {
  components: {
    TheResturantInfo,
  },
}
</script>

<style lang="scss" scoped>
</style>