<template>
    <header>
        <div class="banner"></div>
        <ul class="nav">
              <li v-for="item in choices" :key="item.id">
                <a href="" @click.stop.prevent="change(item.id)" :class="{checked: item.isChecked}">{{item.name}}</a>
              </li>
        </ul>
    </header>
</template>

<script>
export default {
  data () {
    return {
      choices: [
        { id: 0, name: '全国疫情', isChecked: true },
        { id: 1, name: '世界疫情', isChecked: false },
        { id: 2, name: '疫情动态', isChecked: false }
      ]
    }
  },
  methods: {
    change (id) {
      this.choices.some(item => {
        if (item.id === id) {
          item.isChecked = true
        } else {
          item.isChecked = false
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
    header{
      width: 100%;
    }
    .banner{
        width: 100%;
        height: 6.24rem;
        background: url('../assets/imgs/banner.jpg') no-repeat;
        background-size: 100% 6.24rem;
    }

    .checked{
      border-bottom: 3rem / 25 solid #4d79f3;
      font-weight: bold;
    }
    .nav{
        margin: 0;
        padding: 0;
        background-color: #fff;
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        li{
          list-style: none;
          a{
            display: block;
            box-sizing: border-box;
            text-align: center;
            text-decoration: none;
            margin: 0 18.6rem / 25;
            width: 69.45rem / 25;
            height: 48.6rem / 25;
            line-height: 48.6rem / 25;
            font-size: 14rem / 25;
            color: black;
          }
        }
    }
</style>
