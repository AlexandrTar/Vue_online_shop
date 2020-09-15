<template>
  <div class="v-catalog">

    <v-notification
      :messages="messages"
      :timeout="4000"
    />

    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog__link_to_cart">
        <img class="v-catalog__icon_cart" src="../assets/images/Tilda_Icons_3st_cart.svg" alt="Cart"> {{CART.length}}
      </div>
    </router-link>
    <h1>Catalog</h1>
    <div class="v-catalog__list">
      <v-catalog-item
        v-for="product in PRODUCTS"
        :key="product.article"
        :product_data="product"
        @add-to-cart="addToCart"
      />

    </div>
  </div>
</template>

<script>
import vCatalogItem from './v-catalog-item'
import vNotification from './notifications/v-notification'
import {mapActions, mapGetters} from 'vuex'

export default {
  name: "v-catalog",
  data() {
    return {
      messages: []
    }
  },
  components: {
    vCatalogItem,
    vNotification
  },
  computed: {
    ...mapGetters([
      'PRODUCTS',
        'CART'
    ]),
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
    ]),
    addToCart(data) {
      this.ADD_TO_CART(data)
      .then(() => {
        let timeStamp = Date.now().toLocaleString()
        this.messages.unshift(
            {name: 'Product added to cart', id: timeStamp}
        )
      })
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
    .then(res => {
      if(res.data) {
        console.log('data arrived')
      }
    })
  }
}
</script>

<style lang="scss">
  .v-catalog{
    &__list{
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }
    &__link_to_cart {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: $padding*2;
      text-transform: uppercase;

      display: flex;
      justify-content: center;
      align-items: center;
    }
    &__icon_cart{
      width: 40px;
      height: 25px;
    }
  }
</style>