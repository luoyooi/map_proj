<template>
  <div id="app">
    <Header></Header>
    <TotalShow :data="data"></TotalShow>
    <Map :list="data.list"></Map>
    <Analyze :data="data"></Analyze>
  </div>
</template>

<script>
import jsonp from 'jsonp'
import Header from './components/header'
import Map from './components/map'
import TotalShow from './components/totalshow'
import Analyze from './components/analyze'

export default {
  name: 'app',
  data () {
    return {
      data: {}
    }
  },
  components: { Header, Map, TotalShow, Analyze },
  mounted: function () {
    // 使用jsonp请求数据
    jsonp('https://gwpre.sina.cn/interface/fymap2020_data.json?_=1588512211971', {}, (err, result) => {
      if (!err) { // 请求数据成功
        this.data = result.data
      }
    })
  }
}
</script>

<style>
#app {
  width: 15rem;
}
</style>
