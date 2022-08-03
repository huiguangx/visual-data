<template>
  <div>
    <header>
        <h1>大数据可视化</h1>
    </header>
    <section class="container">
        <section class="itemLeft">
            <ItemPage>
                <ItemOne/>
            </ItemPage>
            <ItemPage>
                <ItemTwo/>
            </ItemPage>
        </section>
        <section class="itemCenter">
            <MapPage/>
        </section>
        <section class="itemRight">
            <ItemPage>
                <ItemThree/>
            </ItemPage>
            <ItemPage>
                <ItemFour/>
            </ItemPage>
        </section>
    </section>
  </div>
</template>

<script>
import ItemPage from "@/components/ItemPage.vue"
import ItemOne from "@/components/ItemOne.vue"
import ItemTwo from "@/components/ItemTwo.vue"
import ItemThree from "@/components/ItemThree.vue"
import ItemFour from "@/components/ItemFour.vue"
import MapPage from "@/components/MapPage.vue"
export default {
    components: {
        ItemPage,
        ItemOne,
        ItemTwo,
        ItemThree,
        ItemFour,
        MapPage
    }
}
</script>

<style lang="less">
    header {
        height: 1rem;
        width: 100%;
        background-color: rgba(0, 0, 255, .2);
        h1 {
            font-size: 0.375rem;
            color: #fff;
            text-align: center;
            line-height: 1rem;
        }
    }
    .container {
        // 最大最小宽度
        min-width: 1200px;
        max-width: 2048px;
        margin: 0 auto;
        border: 1px solid red;
        padding: .125rem .125rem 0;
        // 设置flex布局
        display: flex;
        .itemLeft, .itemRight {
            flex: 3;
        }
        .itemCenter {
            flex: 5;
            height: 10.5rpx;
            border: 1px solid blue;
            padding: 0.125rem;
            margin: .25rem;
        }
    }
</style>