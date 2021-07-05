<template>
  <main class="container">
    <TheHeader />
    <TheResturantInfo :dataSource="fooddata" />
  </main>
</template>

<script>
import TheHeader from '@/components/TheHeader.vue';
import TheResturantInfo from '@/components/TheResturantInfo.vue';
import { mapState } from 'vuex';

export default {
  components: {
    TheHeader,
    TheResturantInfo,
  },
  computed: {
    ...mapState(['fooddata']),
  },
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
