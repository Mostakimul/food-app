<template>
  <main class="container">
    <TheHeader />
    <TheResturantInfo />
  </main>
</template>

<script>
import TheHeader from '@/components/TheHeader.vue'
import TheResturantInfo from '@/components/TheResturantInfo.vue'

export default {
  components: {
    TheHeader,
    TheResturantInfo,
  },
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
