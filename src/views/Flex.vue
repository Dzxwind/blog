<template>
  <div class="flex">
    <h1>flex弹性布局</h1>
    <h2>场景1</h2>
    <div class="flex1 father">
      <div class="flex1_i son" v-for="item in 3" :key="item"></div>
    </div>
    <h3>flex:1 auto;</h3>
  </div>
</template>
<script>
export default {
  data() {}
};
</script>
<style lang="scss" scoped>
.flex {
  .father {
    width: 800px;
    height: 200px;
    background-color: #eeeeee;
    margin: 0 auto;
  }
  .son {
    height: 100%;
    background: #42b983;
    border: 1px solid #148351;
  }
  .flex1 {
    display: flex;
    &_i {
      flex: 1 auto;
    }
  }
}
</style>
