<template>
  <div class="cartcontrol" >
    <transition name="move-transition">
      <div class="cart-decrease"  v-show="food.count>0" @click="decreaseCart($event)">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart($event)"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';

  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      addCart(event) {
        if (!event._constructed) {
          return;
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('addCart', event.target);
      },
      decreaseCart(event) {
        if (!event._constructed) {
          return;
        }
        this.food.count--;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    .move-transition-enter
      opacity: 0
      transform: translate3D(48px,0,0)
    .move-transition-enter-active
      transition: all 0.4s linear
    .move-transition-leave-active
      opacity: 0
      transition: all 0.4s linear
      transform: translate3D(48px,0,0)
      .inner
        transition: all 0.4s linear
        transform: rotate(180deg)
    .cart-decrease
      display: inline-block
      .inner
        display: inline-block
        padding: 6px
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
    .cart-count
      display: inline-block
      margin: 0px
      padding-top: 6px
      font-size: 10px
      vertical-align: top
      width: 12px
      line-height: 24px
      text-align: center
      color: rgb(147,153,159)
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
</style>
