<template>
  <nav>
    <ul>
      <li>
        <nuxt-link to="/"><TheLogo /></nuxt-link>
      </li>
      <li><nuxt-link to="/restaurant">Restaurant</nuxt-link></li>
    </ul>
    <nuxt-link to="/cart">Cart</nuxt-link>
  </nav>
</template>

<script>
import TheLogo from '@/components/TheLogo.vue';

export default {
  components: {
    TheLogo,
  },
};
</script>

<style lang="scss" scoped></style>
