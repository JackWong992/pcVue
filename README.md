# pcvue

> A Vue.js project

## 公用组件head-nav
```javascript
App.vue
  <head-nav></head-nav>

import headerNav from '@/components/header-nav.vue'
componets: {
  headerNav: headerNav;
}
公共样式：
  import '@/assets/css/header.css' //全局引入，不是按需加载
```

## 列表页 shop
```javascript
  imports  Shop from '@/views/shop.vue'

  router: [
    {
      path: '/',
      name: Shop,
      componet: Shop
    }
  ]
引入数据： imports from '@/lib/newGoods.js'
利用v-for循环显示商品列表页
```
### 加入购物车 商品列表页功能
```javascript
使用vuex(store>index.js)
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use( Vuex )
let store = new Vuex.Store({
  state: {
    carPanelDate: []
  },
  mulations: {
    addCarPanelData(state, data){
      let boff = true
      state.carPanelData.forEach( (goods)=>{
        if(goods.sku_id ==data.sku_id){
          goods.count++
          b0ff = false
        }
      }) 
      if(b0ff){
        let goodsData = data
        Vue.set( goodData , 'count',1 )
        state.carPanelData.push(goodsData)
      }
    }
  }
})

export default store

路由引入：Store
```

### 商品数量最大值提醒功能
```javascript
  if( goods.sku_id ===data.sku.id ){
    goods.count++
    bOff = false
    if(good.count>goods.limit_num){
      goods.count //limit_num 最大值为5，意思是说超过5就会提醒
    }
  }

商品加入隐藏功能：
  closePrompt(state){
    state.maxOff = false
  },
  showCar (state){
    clearTimeout( state.carTimer )
    state.carShow = true
  },
  hideCar (state){
    state.carTimer = setTimeout(){
      state.carShow = false
    },500
  }

```

## 购物车小球飞入效果
```javascript
  <transition 
    name="ball"
    v-on:before-enter="beforeEnter"
    v-on:enter="enter"
    v-on:after-enter="afterEnter"
    v-bind:css="true">
    <div class="addcart-mask">
      <img class="mask-item">
    </div>
  </transition>

beforeEnter(el){
  let rect = this.ball.el.getBoundClientRect()
  let rectEl = document.getElementsByClassName('ball-rect')[0].getBoundingClientRect()
  let ball = document.getElementsByClassName('mask-item')[0]
  let x = (rectE.left+16)-(rect.left)+(rect.width/2)
}

```

## 购物清单页
```javascript
import Cart from '@/views/cart.vue'
购物车的数据：
computed: {
    carPanelData(){
      return this.$store.state.carPanelData
    },
    count(){
      return this.$store.getter.totleCount
    }
},
methods: {
  delCarPanelHandle(id){
    this.$store.commit('delCarPanelData', id)
  }//删除数据
}

```
### 全选商品
```javascript
  allCheckedGoods(state, allChecked){
    state.carPanelDate.forEach( (goods, index)=>{
      goods.checked = !isallChecked
    })
  }

全选数量：
 checkedCount(){
   let count = 0
   state.carPanelDate.forEach( (goods)=>{
     if(goods.checked){
       count += goods.count
     }
   })
   return count
 }
全选价格：
  checkedPrice(){
    let price = 0 
    state.carPanelData.forEach( (goods)=>{
      if(goods.checked){
        price +=goods.count*goods.price
      }
    })
  }
```
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
