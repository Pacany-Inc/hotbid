<template>
  <div id="wrapper">
    <nav class="navbar is-dark">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item">
          <strong>HotBid</strong>
        </router-link>
        <a
            class="navbar-burger"
            aria-label="menu"
            aria-expanded="false"
            data-target="navbar-menu"
            @click="showMobileMenu = !showMobileMenu"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active': showMobileMenu }">
        <div class="navbar-end">
          <div class="navbar-item">
            <!-- Выпадающий список -->
            <div class="dropdown is-hoverable">
              <div class="dropdown-trigger">
                <button class="button" aria-haspopup="true" aria-controls="dropdown-menu4">
                  <span>Категории</span>
                  <span class="icon is-small">
                    <i class="fas fa-angle-down" aria-hidden="true"></i>
                  </span>
                </button>
              </div>
              <div class="dropdown-menu" id="dropdown-menu4" role="menu">
                <div class="dropdown-content">
                  <router-link to="/estate" class="dropdown-item">Недвижимость</router-link>
                  <router-link to="/vehicles" class="dropdown-item">Транспорт</router-link>
                  <router-link to="/antiques" class="dropdown-item">Антиквариат</router-link>
                  <router-link to="/personal-things" class="dropdown-item">Личные вещи</router-link>
                  <router-link to="/interior" class="dropdown-item">Интерьер</router-link>
                </div>
              </div>
            </div>
            <!-- Конец выпадающего списка -->
          </div>
          <div class="navbar-item">
            <div class="buttons">
              <router-link to="/log-in" class="button is-black">Войти</router-link>

              <router-link to="/cart" class="button is-black">
                <span class="icon"><i class="fas fa-shopping-cart"></i></span>
                <span>Корзина</span>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <section class="section">
      <router-view/>
    </section>

    <footer class="footer">
      <p class="has-text-centered">Copyright (c) 2024</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showMobileMenu: false,
    }
  }
}

</script>

<style lang="scss">
@import '../node_modules/bulma';
</style>
<script setup>
</script>