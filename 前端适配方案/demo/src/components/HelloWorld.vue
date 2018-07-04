<template>
  <div class="hello">
    <!-- <p>红色线为css1像素，绿线为物理1像素；</p>
    <p>HelloWorld会随着设备dpr更改font-size</p> -->
    <p class="text">HelloWorld</p>
    <ul class="items">
      <li class="item border-1px"></li>
      <li class="item border-1px" v-for="item in items" :key="item.id">{{item.msg}}</li>
    </ul>
    <p>----分割线----</p>
    <ul class="items">
      <li class="item-2 border-1px" v-for="item in items" :key="item.id">{{item.msg}}</li>
    </ul>

    <div class="block-wrapper">
      <div class="item-div"></div>
      <div class="block1"></div>
      <div class="block2"></div>
      <div class="block3"></div>
      <div class="block4"></div>
      <div class="block5"></div>
      <div class="block6"></div>
      <div class="block7"></div>
      <div class="block8"></div>
      <div class="block9"></div>
      <div class="block10"></div>
      <div class="abso border-1px">word</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      items: [
        {
          id: 1,
          msg: 'HelloWorld',
        },
        {
          id: 2,
          msg: '111',
        },
        {
          id: 3,
          msg: '111',
        },
      ],
    };
  },
  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import '../common/style/index.scss';
.text {
  @include font-size();
  // font-size: 72px
}

.item {
  font-size: 36px;
  // @include border-top-1px(green);
  @include border-bottom-1px(blue);
  // border-top: 1px solid red;
}
.item-2 {
  font-size: 36px;
  margin: 0.1rem 25%;
  width: 6rem;
  // @include border-top-1px(green);
  @include border-1px;
  // border-top: 1px solid red;
}

.item-div {
  height: 1px;
  width: 100%;
  background: blue;
  transform: scaleY(0.1);
}
.block-wrapper {
  position: relative;
}
.block1 {
  height: 1rem;
  width: 1rem;
  background: #111
}
.block2 {
  height: 1rem;
  width: 2rem;
  background: #eee
}
.block3 {
  height: 1rem;
  width: 3rem;
  background: #222
}
.block4 {
  height: 1rem;
  width: 4rem;
  background: #ddd
}
.block5 {
  height: 1rem;
  width: 5rem;
  background: #333
}
.block6 {
  height: 1rem;
  width: 6rem;
  background: #ccc
}
.block7 {
  height: 1rem;
  width: 7rem;
  background: #444
}
.block8 {
  height: 1rem;
  width: 8rem;
  background: #bbb
}
.block9 {
  height: 1rem;
  width: 9rem;
  background: #555
}
.block10 {
  height: 1rem;
  width: 10rem;
  background: #aaa
}
.abso {
  position: absolute;
  left: 7rem;
  bottom: 7rem;
  width: 2rem;
  height: 1rem;
  @include font-size(28px)
  // background: red;
  // @include border-1px(red)
}
</style>
