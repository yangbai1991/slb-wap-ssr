<template>
  <div class="goods">
    <van-swipe class="goods-swipe">
      <van-swipe-item v-for="thumb in goods.thumb" :key="thumb">
        <img :src="thumb" >
      </van-swipe-item>
    </van-swipe>

    <van-cell-group>
      <van-cell>
        <div class="goods-title">{{ goods.title }}</div>
        <div class="goods-price">{{ formatPrice(goods.price) }}</div>
      </van-cell>
      <van-cell class="goods-express">
        <van-col span="10">运费：{{ goods.express }}</van-col>
        <van-col span="14">剩余：{{ goods.remain }}</van-col>
      </van-cell>
    </van-cell-group>

    <van-cell-group class="goods-cell-group">
      <van-cell value="进入店铺" icon="shop" isLink>
        <template slot="title">
          <span class="van-cell-text">有赞的店</span>
          <van-tag type="danger">官方</van-tag>
        </template>
      </van-cell>
      <van-cell title="线下门店" icon="location" isLink></van-cell>
    </van-cell-group>

    <van-cell-group class="goods-cell-group">
      <van-cell title="查看商品详情" isLink></van-cell>
    </van-cell-group>

    <van-goods-action>
      <van-goods-action-mini-btn icon="chat">
        客服
      </van-goods-action-mini-btn>
      <van-goods-action-mini-btn icon="cart" @click="toCart">
        购物车
      </van-goods-action-mini-btn>
      <van-goods-action-big-btn>
        加入购物车
      </van-goods-action-big-btn>
      <van-goods-action-big-btn primary @click="showBase=true">
        立即购买
      </van-goods-action-big-btn>
    </van-goods-action>

    <van-sku
      v-model="showBase"
      :sku="sku"
      :goods="goods"
      :goodsId="goodsId"
      :hideStock="sku.hide_stock"
      :quota="quota"
      :quotaUsed="quotaUsed"
      :resetStepperOnHide="resetStepperOnHide"
      :disableStepperInput="disableStepperInput"
      @buy-clicked="handleBuyClicked"
      @add-cart="handleAddCartClicked"
    >
      <template slot="sku-actions">
        <div class="van-sku-actions">
          <van-button type="primary" bottomAction @click="handleBuyClicked">下一步</van-button>
        </div>
      </template>
    </van-sku>
  </div>
</template>

<script>
export default {
  data () {
    return {
      showBase: false,
      sku: {
        tree: [
          {
            k: '颜色',
            v: [{
              id: '30349', // skuValueId：规格值id
              name: '红色', // skuValueName：规格值名称
              imgUrl: 'https://img.yzcdn.cn/public_files/2017/10/24/e5a5a02309a41f9f5def56684808d9ae.jpeg'
            },
            {
              id: '1215',
              name: '蓝色',
              imgUrl: 'https://img.yzcdn.cn/public_files/2017/10/24/1791ba14088f9c2be8c610d0a6cc0f93.jpeg'
            }],
            k_s: 's1'
          }
        ],
        list: [
          { id: 1, price: 1200, s1: '30349', stock_num: 19 },
          { id: 2, price: 6600, s1: '1215', stock_num: 2 }
        ],
        price: 100,
        stock_num: 21
      },
      goods: {
        title: '美国伽力果（约680g/3个）',
        price: 1200,
        express: '免运费',
        remain: 19,
        picture: 'https://img.yzcdn.cn/public_files/2017/10/24/1791ba14088f9c2be8c610d0a6cc0f93.jpeg',
        thumb: [
          'https://img.yzcdn.cn/public_files/2017/10/24/e5a5a02309a41f9f5def56684808d9ae.jpeg',
          'https://img.yzcdn.cn/public_files/2017/10/24/1791ba14088f9c2be8c610d0a6cc0f93.jpeg'
        ]
      },
      goodsId: 1,
      quota: 0,
      quotaUsed: 0,
      resetStepperOnHide: false,
      disableStepperInput: false,
      handleBuyClicked: () => {},
      handleAddCartClicked: () => {}
    };
  },
  methods: {
    formatPrice () {
      return '¥' + (this.goods.price / 100).toFixed(2);
    },
    toCart () {
      this.$router.push({ name: 'cart' });
    }
  }
};
</script>

<style lang="scss" scoped>
  .goods {
    padding-bottom: 50px;
    &-swipe {
      img {
        width: 7.5rem;
        height: 7.5rem;
        display: block;
      }
    }
    &-title {
      font-size: 16px;
    }
    &-price {
      color: #f44;
    }
    &-express {
      color: #999;
      font-size: 12px;
      padding: 5px 15px 5px 0;
    }
    &-cell-group {
      margin: 15px 0;
      .van-cell__value {
        color: #999;
      }
    }
  }
</style>
