<template>
  <main class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants</h1>
      <TheSelect @change="selectedRestaurant = $event" />
      <pre>{{ $data }}</pre>
    </div>
    <TheResturantInfo />
  </main>
</template>

<script>
import TheResturantInfo from '@/components/TheResturantInfo.vue';
import TheSelect from '@/components/TheSelect.vue';
export default {
  components: {
    TheSelect,
    TheResturantInfo,
  },
  data() {
    return {
      selectedRestaurant: '',
    };
  },
};
</script>

<style lang="scss" scoped></style>
