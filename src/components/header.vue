<template>
    <header>
        <div class="banner"></div>
        <div class="nav">
            <a href="" v-for="item in choices" :key="item.id" @click.stop.prevent="change(item.id)" :class="{checked: item.isChecked}">
            {{item.name}}
            </a>
        </div>
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
    .banner{
        width: 100%;
        height: 156.07px;
        background: url('../assets/imgs/banner.jpg') no-repeat;
        background-size: auto 156.07px;
    }
    .nav{
        border-top: 1px solid #ccc;
        border-bottom: 1px solid #ccc;
        margin-bottom: 10px;
        a{
            text-decoration: none;
            display: inline-block;
            width: 56px;
            height: 39px;
            line-height: 39px;
            margin: 0 15px;
            font-size: 14px;
            font-weight: bold;
            color: black;

        }

        .checked{
            border-bottom: 3px solid #4d79f3;
        }
    }
</style>
