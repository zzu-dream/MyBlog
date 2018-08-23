---
title:  weex 开发坑点
tags:  [weex 坑点]
categories:  [weex]
date:  2018-06-11 16:17:22
---


``` html
0、div 执行v-for循环的时候 要设置动态宽 自动撑满在iOS上有问题
<div v-for="(itemProduct,index) in productList" :style="{height:sliderHeight,width:brandItemBgWidth}"
     style="align-items: center;justify-content: center;">
1、<text>aaa</text>  该标签一定要写在一行否则native展示不对
2、作为子组件里面的数据源一定要 这样写
data: function () { }   必须加上function 不能做省略
3、引入组件或者工具类
  import PromotionWishLampItemView from './PromotionWishLampItemView.vue’
 import Util from './PromotionUtil.js'
4、引入的子组件要注册
export default {
    components: {
        PromotionWishLampItemView
    },}
5、控件属性进行双向绑定用v-bind 缩写是冒号 :
6、例如生命周期函数created、mounted和methods是并列的函数体，methods存放自定义函数
7、 foreach不支持直接break
//                                _wishLamps.forEach(function (item, index) {
//////                                    foreach不支持直接break
//                                });
8、给某个对象添加属性并赋值的方式
    if (typeof item.itemStyle == 'undefined') {
        console.log('注册中 =====');
        //全局注册
        Vue.set(item, "itemStyle", "1");
    }
9、数组剪切前四个（n个）的方案
    _proList.slice(0, 4);
10、数组添加对象的方式
     _this.productList.push(wishLampDict);
11、css style双向绑定要用花括号
    :style="{height:brandItemCurveHeight,width:brandItemWidth}”
12、json转化成能打印的字符串
var str = JSON.stringify(result);
console.log('qryExclusiveDiscount-backData:' + str);
13、通过某个比例scale计算字体大小 如果不是整形在android上显示有问题 
this.contentFontSize = Math.round(26 * scale);
14、通过某个比例scale计算字体大小 如果不是整形在android上显示有问题   通过向上取整显示个别有问题


通过向下取整 Math.floor 

```




