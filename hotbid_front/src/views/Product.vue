<template>
  <div class="page-product">
    <div class="columns is-multiline">
      <div class="column is-4">
        <figure class="image mb-6">
          <img v-bind:src="product.get_image">
        </figure>


      </div>

      <div class="column is-4">
        <h1 class="title">{{ product.name }}</h1>

        <p>{{ product.description }}</p>
      </div>

      <div class="column is-4">
        <h1 class="title">Статус: Торгуется</h1>

        <p><strong>До окончания торгов: 00:00:00</strong></p>

        <hr>

        <p><strong>Начальная цена: {{ product.price }}РУБ</strong></p>

        <hr>

        <p><strong>Текущая цена: 100 РУБ</strong></p>

        <div class="field has-addons mt-6">
          <div class="control">
            <input type="number" class="input no-spinner" placeholder="Введите сумму" v-model="quantity">
          </div>

          <div class="control">
            <a class="button is-dark" @click="addToCart">Сделать ставку</a>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
  name: 'Product',
  data() {
    return {
      product: {},
      quantity: 0
    }
  },
  mounted() {
    this.getProduct()

  },
  methods: {
    async getProduct() {
      this.$store.commit('setIsLoading', true)

      const category_slug = this.$route.params.category_slug
      const product_slug = this.$route.params.product_slug

      await axios
          .get(`/api/v1/products/${category_slug}/${product_slug}`)
          .then(response => {
            this.product = response.data

            document.title = this.product.name + ' | Аукцион HotBid'
          })
          .catch(error => {
            console.log(error)
          })

      this.$store.commit('setIsLoading', false)
    },
    addToCart() {
      if (isNaN(this.quantity) || this.quantity < 1) {
        this.quantity = 1
      }

      const item = {
        product: this.product,
        quantity: this.quantity,
      }

      this.$store.commit('addToCart', item)

      toast({
        message: 'Ставка принята, товар успешно добавлен в корзину!     ',
        type: 'is-success',
        dismissible: true,
        pauseOnHover: true,
        duration: 2000,
        position: 'bottom-right',
      })
    }
  }
}
</script>

<style scoped>
img {
  height: 30vw;
  width: auto;
}
.no-spinner::-webkit-outer-spin-button,
.no-spinner::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.no-spinner {
  -moz-appearance: textfield;
}
</style>