<template>
  <div>
    <div class="header">
      <h1>Landlord</h1>
      <span>Fall 2019 Menswear</span>
      <ul>
        <li :class="{'active':!activeTag }" @click="activeTag=false">COLLECTION</li>
        <li :class="{'active':activeTag }" @click="activeTag=true">ALL SEASON</li>
      </ul>
    </div>

    <div class="body">
      <div class="wrap">
        <div :key="index" class="item" v-for="(item,index) in 3">
          <img :src="'../../../static/images/pictures/'+(item+1)+'.jpg'">
        </div>
      </div>
      <div class="wrap">
        <div :key="index" class="item" v-for="(item,index) in 3">
          <img :src="'../../../static/images/pictures/'+(item+4)+'.jpg'">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// Use Vuex
import store from './store'

export default {
  data() {
    return {
      activeTag: false
    }
  },

  methods: {
    onPullDownRefresh() {
      aa = Math.random(100)
      console.log(aa)
    }
  }
}
</script>

<style lang="scss">
.header {
  text-align: center;
  font-weight: 500;

  span {
    font-size: 12px;
    font-weight: 400;
  }
  ul {
    display: flex;
    margin-top: 5px;
    li {
      flex: 1;
      text-align: center;
      font-size: 14px;
      color: grey;
      &.active {
        color: rgb(117, 14, 14);
      }
    }
  }
}
.wrap {
  display: flex;
  margin-top: 5px;
  .item {
    flex: 1;
    height: 200px;
    margin-right: 5px;
    &:last-child {
      margin-right: 0;
    }
  }
}
img {
  width: 100%;
  height: 100%;
}
</style>
