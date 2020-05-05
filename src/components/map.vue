<template>
    <div class="container">
      <div class="map-container">
        <div ref="now_map" class="map" :class="{showMap: isNowShow}"></div>
        <div ref="cal_map" class="map" :class="{showMap: isCalShow}"></div>
      </div>
      <div class="toggle">
        <el-row>
          <el-button :class="{showBtn: isNowShow}" plain @click="showNow">现存数据</el-button>
          <el-button :class="{showBtn: isCalShow}" plain @click="showCal">累计数据</el-button>
        </el-row>
      </div>

    </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts/map/js/china.js'

export default {
  props: ['list'],
  data () {
    return {
      isNowShow: true,
      isCalShow: false
    }
  },
  methods: {
    showNow () {
      this.isNowShow = true
      this.isCalShow = false
    },
    showCal () {
      this.isNowShow = false
      this.isCalShow = true
    },
    showMap (container, data, type) {
      const myChart = echarts.init(container)

      const option = {
        title: {
          text: '疫情动态',
          subtext: '数据来源于新浪',
          sublink: 'https://news.sina.cn/zt_d/yiqing0121'
        },
        // 视觉映射组件
        visualMap: {
          // 类型
          type: 'piecewise',
          itemWidth: 10,
          itemHeight: 10,
          orient: 'horizontal',
          // 自定义分段数
          pieces: [
            { max: 0, label: '0', color: '#ffffff' },
            { min: 1, max: 9, label: '1-9', color: '#fff4ef' },
            { min: 10, max: 99, label: '10-99', color: '#ffe6da' },
            { min: 100, max: 999, label: '100-999', color: '#fdb19b' },
            { min: 1000, max: 9999, label: '1000-9999', color: '#de512f' },
            { min: 10000, label: '≥10000', color: '#970a0f' }
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
          zoom: 0.8,
          layoutCenter: ['50%', '50%'],
          layoutSize: 400,
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
  watch: {
    list: function () {
      if (this.list) {
        // 现存数据
        const nowData = []

        // 累计数据
        const calData = []

        // 封装数据
        this.list.forEach(item => {
          nowData.push({ name: item.name, value: item.econNum })
          calData.push({ name: item.name, value: item.value })
        })

        // 渲染现存数据
        this.showMap(this.$refs.now_map, nowData, '现存')
        // 渲染累计数据
        this.showMap(this.$refs.cal_map, calData, '累计')
      }
    }
  }
}
</script>

<style lang="less" scoped>
  .container{
    margin: 10px 5px;
  }

  .map-container{
    position: relative;
    height: 400px;
    box-sizing: border-box;
    background-color: #fff;
    border-radius: 5px 5px 0 0;

    div.map{
      width: 100%;
      height: 100%;
      position: absolute;
      left: 0;
      top: 0;
      z-index: 1;
      background-color: #fff;
    }
  }

  .toggle{
      background-color: #fff;
      border-top: .01rem solid #ccc;
      border-radius: 0 0 5px 5px;
      padding: 2px 5px 5px;
  }

  .showMap{
    z-index: 100 !important;
  }

  .showBtn{
    border: 1px solid #4ea4fb;
    color: #4ea4fb;
    font-weight: bold;
  }
</style>
