<template>
  <div id="app">
    <div id="nav">
      <template v-for="(item,index) in routerList">
        <router-link :to="item.path" :key="item.name">{{item.name}}</router-link> <span v-if="index < routerList.length - 1" :key="item.name"> | </span>
      </template>
    </div>
    <router-view/>
  </div>
</template>
<script>
export default {
  computed:{
    routerList(){
      return this.$router.options.routes
    }
  },
}
</script>
<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
