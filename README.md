# wrapScroll
#vue轮播图组件<br>
#组件使用方法
```javascript
<WrapScroll :items="items" :width="1152" :proChildWidth="176" :proGap='16' :proSrcollNum='3' :toUrl=""></WrapScroll>
items:[
        {imageUrl:[require("./assets/1 (1).png")],nickname:'aaaa'},
        {imageUrl:[require("./assets/1 (2).png")],nickname:'qqqqq'},
        {imageUrl:[require("./assets/1 (3).png")],nickname:'wwwww'},
        {imageUrl:[require("./assets/1 (4).png")],nickname:'eeeee'},
        {imageUrl:[require("./assets/1 (5).png")],nickname:'atttttaaa'},
        {imageUrl:[require("./assets/1 (6).png")],nickname:'aayyyyaa'},
        {imageUrl:[require("./assets/1 (7).png")],nickname:'yyyy'},
        {imageUrl:[require("./assets/1 (8).png")],nickname:'aauuuuaa'},
        {imageUrl:[require("./assets/1 (9).png")],nickname:'uuuu'}
      ]
items:{//滚动的元素
          type:Array,
          default(){
              return[]
          }
      },
width:{//页面展示的宽度
    type:Number,
    default:1200
},
proGap:{//每个滚动元素之间的间隔
    type:Number,
    default:20
},
proSrcollNum:{//一次滚动的元素的个数
    type:Number,
    default:2
},
proChildWidth:{//滚动的元素的宽度
type:Number,
default:180
},
toUrl:{//跳转地址
type:String,
default:""
}
```
