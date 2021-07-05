<template>
  <main class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants</h1>
      <TheSelect @change="selectedRestaurant = $event" />
      <!-- <pre>{{ $data }}</pre> -->
    </div>
    <TheResturantInfo :dataSource="filteredRestaurant" />
  </main>
</template>

<script>
import TheResturantInfo from '@/components/TheResturantInfo.vue';
import TheSelect from '@/components/TheSelect.vue';
import { mapState } from 'vuex';

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
  computed: {
    ...mapState(['fooddata']),
    filteredRestaurant() {
      if (this.selectedRestaurant) {
        return this.fooddata.filter((el) => {
          let name = el.name.toLowerCase();
          return name.includes(this.selectedRestaurant);
        });
      }

      return this.fooddata;
    },
  },
};
</script>

<style lang="scss" scoped></style>
