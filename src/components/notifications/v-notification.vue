<template>
  <div class="v-notification">
    <transition-group
        name="v-transition-animate"
        class="messages_list"
    >
      <div
          v-for="message in messages"
          :key="message.id"
          class="v-notification__content"
      >
        <div class="content__text">
          <span class="content__text_message">{{message.name}}</span>
          <span class="content__text_check">&#10003;</span>
        </div>

      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
name: "v-notification",
  props: {
  messages: {
    type: Array,
    default() {
      return []
      }
    },
    timeout: {
    type: Number,
      default() {
        return 3000
      }
    }
  },
  methods: {
    hideNotification() {
      let vm = this
      if(this.messages.length) {
        setTimeout( function () {
          vm.messages.splice(vm.messages.length - 1, 1)
        }, vm.timeout)
      }
    }
  },
  watch: {
    messages() {
      this.hideNotification()
    }
  },
  mounted() {
    this.hideNotification()
  }
}
</script>

<style lang="scss">
.v-notification {
  position: fixed;
  top: 80px;
  right: 16px;
  z-index: 10;

  &__content {
    padding: 16px;
    color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 50px;
    margin-bottom: 16px;
    background: #000;
  }
}
.content__text_check {
  margin-left: 15px;
}

.v-transition-animate {
  &-enter {
    transform: translateX(120px);
    opacity: 0;
  }
  &-enter-active {
    transition: all .6s ease;
  }
  &-enter-to {
    opacity: 1;
  }

  &-leave {
    height: 50px;
    opacity: 1;
  }
  &-liave-active {
    transition: transform .6s ease, opacity .6s, height .6s .2s;
  }
  &-liave-to {
    height: 0;
    transform: translateX(120px);
    opacity: 0;
  }

  &-move {
    transition: transform .6s ease;
  }
}
</style>