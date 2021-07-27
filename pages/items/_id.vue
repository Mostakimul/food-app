<template>
  <main class="container">
    <section
      class="image"
      :style="`background: url(/${currentItem.img}) no-repeat center center`"
    ></section>
    <section class="details">
      <h1>{{ currentItem.item }}</h1>
      <h3>Price: ${{ currentItem.price.toFixed(2) }}</h3>

      <div class="quantity">
        <input type="number" min="1" v-model="count" />
        <button @click="addToCart" class="primary">
          Add to Cart - ${{ combinedPrice }}
        </button>
      </div>

      <fieldset v-if="currentItem.options">
        <legend>
          <h3>options</h3>
        </legend>
        <div v-for="option in currentItem.options" :key="option">
          <input
            type="radio"
            name="option"
            :id="option"
            :value="option"
            v-model="$v.itemOptions.$model"
          />
          <label :for="option">{{ option }}</label>
        </div>
      </fieldset>

      <fieldset v-if="currentItem.addOns">
        <legend>
          <h3>Add Ons</h3>
        </legend>
        <div v-for="addon in currentItem.addOns" :key="addon">
          <input
            type="checkbox"
            name="addon"
            :id="addon"
            :value="addon"
            v-model="$v.itemAddons.$model"
          />
          <label :for="addon">{{ addon }}</label>
        </div>
      </fieldset>
      <!-- After submission -->
      <TheToast v-if="cartSubmitted">
        Order submitted!!! <br />
        Checkout more!
        <nuxt-link to="/restaurant">restaurant</nuxt-link></TheToast
      >
      <!-- If found any error -->
      <TheToast v-if="errors">
        Please select options and <br />
        addons before adding to cart.
        <nuxt-link to="/restaurant">restaurant</nuxt-link></TheToast
      >

      <section class="options">
        <h3>Description</h3>
        <p>{{ currentItem.description }}</p>
      </section>
    </section>
  </main>
</template>

<script>
import { mapState } from 'vuex';
import TheToast from '@/components/TheToast.vue';
import { required } from 'vuelidate/lib/validators';

export default {
  components: {
    TheToast,
  },
  data() {
    return {
      id: this.$route.params.id,
      count: 1,
      itemOptions: '',
      itemAddons: [],
      itemSizeAndCost: [],
      cartSubmitted: false,
      errors: false,
    };
  },
  // Validations
  validations: {
    itemOptions: {
      required,
    },
    itemAddons: {
      required,
    },
  },
  // Methods
  methods: {
    addToCart() {
      let formOutput = {
        item: this.currentItem.item,
        count: this.count,
        options: this.itemOptions,
        addOns: this.itemAddons,
        combinedPrice: this.combinedPrice,
      };
      // check if any error
      let addOnError = this.$v.itemAddons.$invalid;
      let optionError = this.currentItem.options
        ? this.$v.itemOptions.$invalid
        : false;

      if (addOnError || optionError) {
        this.errors = true;
      } else {
        this.errors = false;
        this.cartSubmitted = true;
        // For Store
        this.$store.commit('addToCart', formOutput);
      }
    },
  },
  // Computed
  computed: {
    ...mapState(['fooddata']),
    currentItem() {
      let result;

      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          if (this.fooddata[i].menu[j].id == this.id) {
            result = this.fooddata[i].menu[j];
            break;
          }
        }
      }
      return result;
    },
    combinedPrice() {
      let total = this.count * this.currentItem.price;
      return total.toFixed(2);
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 1000px;
  margin: 100px auto;
  display: grid;
  grid-template-columns: 400px 1fr;
  grid-template-rows: 400px 1fr;
  gap: 60px;
  line-height: 2;
}
.image {
  grid-area: 1 / 1 / 2 / 2;
  background-size: cover;
}
.details {
  grid-area: 1 / 2 / 2 / 3;
  position: relative;
}
.options {
  grid-area: 2 / 1 / 3 / 2;
}
</style>
