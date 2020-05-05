<template>
    <div class="container">
        <AnalyzeTitle :titles="titles"></AnalyzeTitle>
        <div class="tendmap">
            <div ref="linemap"></div>
        </div>
    </div>
</template>

<script>
import AnalyzeTitle from './analyzeTitle'
import echarts from 'echarts'
export default {
  props: ['data'],
  data () {
    return {
      titles: { main_title: '全国疫情现存趋势图', sub_title: '' }
    }
  },
  components: { AnalyzeTitle },
  watch: {
    data: function () {
      if (!this.data.historylist) return

      const date = this.data.historylist.map(item => {
        return item.date
      }).reverse()

      const cnEconNum = this.data.historylist.map(item => {
        return item.cn_econNum
      }).reverse()

      const wjwSusNum = this.data.historylist.map(item => {
        return item.wjw_susNum
      }).reverse()

      const option = {
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['现存确诊', '现存疑似']
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: date
        },
        yAxis: {
          name: '人数',
          type: 'value',
          splitNumber: 6,
          axisLabel: {
            formatter: function (value) {
              return value / 10000 + '万'
            }
          }
        },
        series: [
          {
            name: '现存确诊',
            type: 'line',
            animation: false,
            data: cnEconNum
          },
          {
            name: '现存疑似',
            type: 'line',
            animation: false,
            data: wjwSusNum
          }
        ]
      }

      const myChart = echarts.init(this.$refs.linemap)
      myChart.setOption(option)
    }
  }
}
</script>

<style lang="less" scoped>
    .container{
        margin: 10px 5px;
        width: auto;
        background-color: #fff;
        border-radius: 5px;
    }

    .tendmap{
        width: 100%;
        div{
            width: 100%;
            height: 300rem / 25;
        }
    }
</style>
