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

      <div
          class="column is-3"
          v-for="product in latestProducts"
          v-bind:key="product.id"
      >
        <div class="box">
          <figure class="image mb-4">
            <img v-bind:src="product.get_thumbnail">
          </figure>

          <h3 class="is-size-4">{{ product.name }}</h3>
          <p class="is-size-6 has-text-grey">{{ product.price }} РУБ</p>

          <router-link v-bind:to="product.get_absolute_url" class="button is-dark mt-4">Подробнее</router-link>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HomeView',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
  },
  mounted() {
    this.getLatestProducts()
  },
  methods: {
    getLatestProducts() {
      axios
          .get('/api/v1/latest-products/')
          .then(response => {
            this.latestProducts = response.data
          })
          .catch(error => {
            console.log(error)
          })
    }
  }
}
</script>

<style scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</style>
