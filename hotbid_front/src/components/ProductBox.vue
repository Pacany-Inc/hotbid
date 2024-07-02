<template>
  <div class="column is-3">
    <div class="box">
      <figure class="image-container mb-4">
        <img v-bind:src="product.get_thumbnail" class="image">
      </figure>

      <h3 class="is-size-4">{{ product.name }}</h3>
      <p class="is-size-6 has-text-grey">{{ product.price }} РУБ</p>

      <router-link v-bind:to="product.get_absolute_url" class="button is-dark mt-4">Подробнее</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductBox',
  props: {
    product: Object
  }
}
</script>

<style scoped>
.image-container {
  width: 100%;
  padding-top: 100%; /* This gives the container a 1:1 aspect ratio */
  position: relative;
  overflow: hidden;
}

.image-container .image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover; /* Ensures the image covers the container while maintaining its aspect ratio */
}
</style>
