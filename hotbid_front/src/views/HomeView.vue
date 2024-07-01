<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Добро пожаловать на HotBid
        </p>
        <p class="subtitle">
          Лучший онлайн аукцион!
        </p>
      </div>
      </section>

    <div class="column is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Новинки</h2>
      </div>

      <ProductBox
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" />

    </div>
  </div>
</template>

<script>
import axios from 'axios'

import ProductBox from "@/components/ProductBox.vue";
export default {
  name: 'HomeView',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
    ProductBox,
  },
  mounted() {
    this.getLatestProducts()

    document.title = 'HotBid - Лучший онлайн аукцион в СНГ'
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit('setIsLoading', true)

      await axios
          .get('/api/v1/latest-products/')
          .then(response => {
            this.latestProducts = response.data
          })
          .catch(error => {
            console.log(error)
          })

      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>
