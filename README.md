# wrapScroll
#vue轮播图组件
#组件使用方法
(```)
<WrapScroll :items="items" :width="1152" :proChildWidth="176" :proGap='16' :proSrcollNum='3' :toUrl=""></WrapScroll>
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
(```)
