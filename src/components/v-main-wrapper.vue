<template>
  <div class="v-main-wrapper">
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>


<script>

  export default{
    name: 'v-main-wrapper',
    props: {},
    data() {
      return{
        title: "Main Wrapper"
      }
    },
    methods: {},
    watch: {},
    mounted() {}
  }
</script>


<style>
.v-main-wrapper{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 900px;
  margin: 0 auto;
}
</style>