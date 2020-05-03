<template>
    <div class="map-container">
      <div ref="now_map" class="map"></div>
      <div ref="cal_map" class="map" v-show="isShow"></div>
    </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts/map/js/china.js'
import jsonp from 'jsonp'

export default {
  data () {
    return {
      isShow: false
    }
  },
  methods: {
    showMap (container, data, type) {
      const myChart = echarts.init(container)

      const option = {
        title: {
          text: '疫情地图',
          subtext: '数据来源于新浪',
          sublink: 'https://voice.baidu.com/act/newpneumonia/newpneumonia/?from=osari_pc_1'
        },
        // 视觉映射组件
        visualMap: {
          // 类型
          type: 'piecewise',
          itemWidth: 13,
          itemHeight: 8,
          // 自定义分段数
          pieces: [
            { max: 0, label: '0', color: '#ffffff' },
            { min: 1, max: 9, label: '1-9', color: '#ffe5db' },
            { min: 10, max: 99, label: '10-99', color: '#ff9985' },
            { min: 100, max: 999, label: '100-999', color: '#f57567' },
            { min: 1000, max: 9999, label: '1000-9999', color: '#e64546' },
            { min: 10000, label: '≥10000', color: '#b80909' }
          ],
          textStyle: {
            fontSize: 9
          }
        },
        tooltip: {
          trigger: 'item',
          formatter: '地区：{b}<br/>' + type + '：{c0}'
        },
        series: {
          type: 'map',
          map: 'china',
          zoom: 0.7,
          layoutCenter: ['50%', '50%'],
          layoutSize: 500,
          label: {
            show: true,
            fontSize: 7
          },
          data: data
        }
      }

      myChart.setOption(option)
    }
  },
  mounted: function () {
    // 使用jsonp请求数据
    jsonp('https://gwpre.sina.cn/interface/fymap2020_data.json?_=1588512211971', {}, (err, data) => {
      if (!err) { // 请求数据成功
        // 现存数据
        const nowData = []

        // 累计数据
        const calData = []

        // 封装数据
        data.data.list.forEach(item => {
          nowData.push({ name: item.name, value: item.econNum })
          calData.push({ name: item.name, value: item.value })
        })

        // 渲染现存数据
        this.showMap(this.$refs.now_map, nowData, '现存')
        // 渲染累计数据
        this.showMap(this.$refs.cal_map, calData, '累计')
      }
    })
  }
}

</script>

<style lang="less" scoped>
  .map-container{
    position: relative;
    margin: 0 auto;
    width: 100%;
    height: 400px;
    border: 1px solid black;
    box-sizing: border-box;

    div.map{
      width: 100%;
      height: 100%;
      position: absolute;
      left: 0;
      top: 0;
    }
  }

</style>
