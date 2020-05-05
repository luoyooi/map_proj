<template>
    <div class="container">
        <AnalyzeTitle :titles="titles"></AnalyzeTitle>
        <div class="items">
            <ul>
                <li>
                    <p>现存确诊</p>
                    <p>{{data.econNum}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.addecon_new:""}}</span></p>
                </li>
                <li>
                    <p>累计境外输入</p>
                    <p>{{data.jwsrNum}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.addjwsr:""}}</span></p>
                </li>
                <li>
                    <p>现存无症状</p>
                    <p>{{data.asymptomNum}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.addasymptom:""}}</span></p>
                </li>
                <li>
                    <p>现存重症确诊</p>
                    <p>{{data.heconNum}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.addhecon_new:""}}</span></p>
                </li>
                <li>
                    <p>累计确诊</p>
                    <p>{{data.gntotal}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.addcon_new:""}}</span></p>
                </li>
                <li>
                    <p>累计死亡</p>
                    <p>{{data.deathtotal}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.adddeath_new:""}}</span></p>
                </li>
                <li>
                    <p>累计治愈</p>
                    <p>{{data.curetotal}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.addcure_new:""}}</span></p>
                </li>
                <li>
                    <p>现存疑似</p>
                    <p>{{data.sustotal}}</p>
                    <p>较昨日<span>{{data.add_daily?data.add_daily.wjw_addsus_new:""}}</span></p>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import AnalyzeTitle from './analyzeTitle'
export default {
  props: ['data'],
  data () {
    return {
      titles: {}
    }
  },
  components: { AnalyzeTitle },
  watch: {
    data: function () {
      this.titles = { main_title: '全国(含港澳台)', sub_title: this.data.times + '数据统计' }
    }
  }
}
</script>

<style lang="less" scoped>
    .container{
        margin: 10px 5px;
        background-color: #fff;
        border-radius: 5px;
    }

    .items{
        ul{
            display: flex;
            flex-flow: row wrap;
            justify-content: space-between;
            align-content: space-between;
            text-align: center;
            li{
                list-style: none;
                width: 25%;
                margin-bottom: 17.36rem / 25;
                p:nth-of-type(1){
                    color: #393939;
                    font-size: 12.4rem / 25;
                }
                p:nth-of-type(2){
                    font-size: 26.04rem / 25;
                    font-weight: bold;
                }
                p:nth-of-type(3){
                    font-size: 12.4rem / 25;
                    color: #999;
                    span{
                        color: #666;
                        font-weight: bold;
                    }
                }
                //循环生成字体颜色
                @colorList: #ff3535,#fe6b23, #fe9986, #8a121c, #b10000, #4b4b4b, #13b593, #a36fff;
                @n: length(@colorList);

                &:nth-of-type(1) p:nth-of-type(2){
                    color: extract(@colorList, 1);
                }

                &:nth-of-type(2) p:nth-of-type(2){
                    color: extract(@colorList, 2);
                }

                &:nth-of-type(3) p:nth-of-type(2){
                    color: extract(@colorList, 3);
                }

                &:nth-of-type(4) p:nth-of-type(2){
                    color: extract(@colorList, 4);
                }

                &:nth-of-type(5) p:nth-of-type(2){
                    color: extract(@colorList, 5);
                }

                &:nth-of-type(6) p:nth-of-type(2){
                    color: extract(@colorList, 6);
                }

                &:nth-of-type(7) p:nth-of-type(2){
                    color: extract(@colorList, 7);
                }

                &:nth-of-type(8) p:nth-of-type(2){
                    color: extract(@colorList, 8);
                }
            }
        }
    }
</style>
