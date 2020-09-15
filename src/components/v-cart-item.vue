<template>
  <div class="v-cart-item">
    <img class="v-cart-item__image"
         :src=" require('../assets/images/' + cart_item_data.image)"
         alt="img"
    >
    <div class="v-cart-item__info">
      <p>Name: <span class="inf">{{cart_item_data.name}}</span></p>
      <p>Price: <span class="inf">{{cart_item_data.price}}</span></p>
      <p>Article: <span class="inf">{{cart_item_data.article}}</span></p>
    </div>

    <div class="v-cart-item__quantity">

<!--      <div class="quantity__title">Q-ty:</div>-->

      <div class="quantity__content">
        <span class="quantity__btn" @click="decrementItem">-</span>
        {{cart_item_data.quantity}}
        <span class="quantity__btn" @click="incrementItem">+</span>
      </div>
    </div>
    <div class="v-cart-item__btn">
      <button class="btn" @click="deleteFromCart">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-cart-item.vue",
  props: {
    cart_item_data: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  mounted() {
    this.$set(this.cart_item_data, 'quantity', 1)
  },
  methods: {
    deleteFromCart() {
      this.$emit('delete-from-cart')
    },
    decrementItem() {
      this.$emit('decrement')
    },
    incrementItem() {
      this.$emit('increment')
    }
  }
}
</script>

<style lang="scss">
.v-cart-item{
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 0 8px 0 #e0e0e0;
  padding: $padding*2;
  margin-bottom: $margin*2;

  min-width: 600px;
  &__image{
    height: 140px;
   }
  .quantity__btn {
    width: 5px;
    height: 5px;
    margin: 0 5px;

    &:hover {
      color: black;
      box-shadow: 0 0 8px 0 #e0e0e0;
    }
  }

}

.quantity__title{
  margin-bottom: 15px;
}
.quantity__btn {
  cursor: pointer;
  font-weight: 700;
  padding: 10px;

}
.inf {
  font-weight: 700;
}
</style>