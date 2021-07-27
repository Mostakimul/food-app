<template>
  <nav>
    <ul>
      <li>
        <nuxt-link to="/"><TheLogo /></nuxt-link>
      </li>
      <li><nuxt-link to="/restaurant">Restaurant</nuxt-link></li>
    </ul>
    <div v-if="cartCount > 0" class="smallnum">{{ cartCount }}</div>
    <nuxt-link to="/cart">Cart</nuxt-link>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex';
import TheLogo from '@/components/TheLogo.vue';

export default {
  components: {
    TheLogo,
  },
  computed: {
    ...mapGetters(['cartCount']),
  },
};
</script>

<style lang="scss" scoped></style>
