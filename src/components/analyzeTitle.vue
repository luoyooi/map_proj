<template>
    <div class="container">
        <span>{{titles? titles.main_title: ""}}</span>
        <span>{{titles? titles.sub_title: ""}}</span>
    </div>
</template>

<script>
export default {
  props: ['titles']
}
</script>

<style lang="less" scoped>
    .container{
        background-color: #fff;

        span{
            padding-left: 6rem / 25;
        }

        span:nth-of-type(1){
            font-size: 19.84rem / 25;
            color: #4d79f3;
            font-weight: bold;
            border-left: 3px solid #4d79f3;
        }

        span:nth-of-type(2){
            font-size: 12.4rem / 25;
            color: #777;
        }
    }
</style>
