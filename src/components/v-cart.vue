<template>
  <div class="v-cart">
    <router-link :to="{name: 'catalog'}">
      <div class="v-catalog__link_to_cart btn_back">
        Back
      </div>
    </router-link>
    <h2>Cart</h2>
    <p v-if="!cart_data.length">There are no products in cart...</p>
    <v-cart-item
      v-for="(item, index) in cart_data"
      :key="item.article"
      :cart_item_data="item"
      @delete-from-cart="deleteFromCart(index)"
      @increment="increment(index)"
      @decrement="decrement(index)"
    />
    <div class="v-cart__total">
      <p class="total_name">Total:</p>
      <p>{{cartTotalCost}} P.</p>
    </div>
  </div>
</template>

<script>
import vCartItem from './v-cart-item'
import {mapActions} from 'vuex'

export default {
  name: "v-cart",
  components: {
    vCartItem
  },
  props: {
    cart_data: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  computed: {
    cartTotalCost() {
      return this.cart_data.reduce((res, item) => res + item.price * item.quantity, 0)
    }
  },
  methods: {
    ...mapActions([
        'DELETE_FROM_CART',
      'INCREMENT_CART_ITEM',
      'DECREMENT_CART_ITEM'
    ]),

    deleteFromCart(index) {
      this.DELETE_FROM_CART(index)
    },

    increment(index) {
      this.INCREMENT_CART_ITEM(index)
    },
    decrement(index) {
      this.DECREMENT_CART_ITEM(index)
    }
  }
}
</script>

<style lang="scss">
.v-cart{
  margin-bottom: 100px;
  &__total{
    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;
    padding: $padding*3;
    display: flex;
    justify-content: center;
    box-shadow: 0 0 16px 0 #e0e0e0;
    background: white;
    font-weight: 700;
    font-size: 20px;
  }
}
.total_name{
  margin-right: $margin*2;
}
.btn_back {
  border: 1px solid black;
  padding: $padding*1.5;
  color: black;
  transition: all .2s linear;

  &:hover {
    background: black;
    color: white;
  }
}
</style>