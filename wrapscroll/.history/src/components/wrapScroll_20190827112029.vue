<template>
  <div class="wrap_scroll"  v-if="items.length>0">
        <div class="wrap-scroll_content">
            <ul class="wrap-scroll_list" id="wrap-scroll_list" style="left:0px;" @mousedown="drag_scroll" >
                    <li v-for="(item, index) in items" :key="index" >
                        <img :src="item.imageUrl[0]" class="wrap-scroll_img"  @click="jumpToDetail(item.playerNo)"/>
                        <div class="hot-recommend_txt" :title="item.nickname" >{{item.nickname}}</div>
                    </li>
                </ul>
        </div>
        <div class="wrap-scroll_btn scroll-left_btn"><i @click="scroll_pre" class="iconfont iconzuo"></i></div>
        <div class="wrap-scroll_btn scroll-right_btn"><i @click="scroll_next" class="iconfont iconzuo1"></i></div>
    </div>
</template>

<script>
export default {
  name: '',
  data() {
    return {
        doc:'',//外层元素
        child:'',//里面滚动的元素
        childLen:0,//里面滚动的元素个数
        childWidth:0,//滚动元素的宽度
        allWidth:0,//滚动元素总宽度
        showWidth:0,//页面展示的宽度
        showWidth:0,//页面展示的宽度
        gap:0,////滚动元素之间的间隔
        srcollNum:0,//一次滚动的元素个数
        scrollWidth:0,//每次滚动一个元素的宽度
        left:0,//外层元素的左边距离
        nextW:0,//next滚动宽度
        preW:0,//pre滚动宽度

    };
  },
  props:{
      items:{
          type:Array,
          default(){
              return[]
          }
      },
      width:{//页面展示的宽度
          type:Number,
          default:1152
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
    //   winWidth:{//展示的窗口宽度
    //       type:Number,
    //      default:1200
    //   },
      toUrl:{//跳转地址
        type:String,
        default:""
      }
  },
  mounted(){
       if(this.items.length>0){
            this.getDom();
            document.getElementsByClassName('wrap-scroll_content')[0].style.width=this.width+'px';//页面展示的容器宽度
            document.getElementsByClassName('wrap_scroll')[0].style.width=this.wrapWidth+'px';//页面展示的容器宽度
            // document.getElementsByClassName('wrap-scroll_content')[0].style.marginLeft=Math.round(this.winWidth-this.width)/2 +'px';//页面展示的容器左边距
            let child = document.getElementById('wrap-scroll_list').children;
            let gap =Math.round(this.proGap/2);
            for(let i=0;i<child.length;i++){
                child[i].style.width=this.proChildWidth+'px';//每个滚动元素的宽度
                child[i].style.marginLeft=gap +'px';//每个滚动元素的左边距
                child[i].style.marginRight=gap +'px';//每个滚动元素的右边距
            }
       }
  },
  methods: {
      getDom(){
            this.doc=document.getElementById('wrap-scroll_list');//外层元素
            this.child=this.doc.getElementsByTagName("li");//里面滚动的元素
            this.childLen=this.child.length;////里面滚动的元素个数
            this.childWidth= this.child[0].offsetWidth;//滚动元素的宽度
            this.showWidth=this.width;//页面展示的宽度
            this.wrapWidth=Number(this.width) + 40;//页面展示的宽度
            this.gap=this.proGap;//滚动元素之间的间隔
            this.srcollNum=this.proSrcollNum;//一次滚动的元素个数
            this.scrollWidth = (Number(this.childWidth)+this.gap);//每次滚动一个元素的宽度
            this.allWidth=this.scrollWidth*this.childLen;//总共需要滚动的宽度
            this.scrollW=this.scrollWidth*this.srcollNum;//每次正常滚动一次的宽度
            this.left = Number(this.doc.style.left.slice(1,this.doc.style.left.indexOf("px")));//外层元素的左边距离
      },
    scroll_next(){
        this.getDom();
        let remainDis = this.allWidth-(this.left+this.showWidth);//剩下需要滚动的距离
        if(remainDis<this.scrollW && remainDis > 0){//如果剩下滚动的距离小于一次正常滚动的距离
            this.nextW = this.allWidth - this.showWidth;
            this.doc.style.left  = `-${this.nextW}px`;
        }else if((this.left+this.showWidth) == this.allWidth){//left距离加上页面展示的距离等于总共需要滚动的宽度
            this.nextW = 0;
            this.doc.style.left  = `-${this.nextW}px`;
        }else{
            this.nextW = this.left+this.scrollW;//left距离加上正常一次滚动的宽度
            this.doc.style.left  = `-${this.nextW}px`;
        }
    },
    scroll_pre(){
        this.getDom();
        if(this.left == 0){//如果左边距离为0就直接跳到最后一页
            this.preW=this.allWidth - this.showWidth;
            this.doc.style.left  = `-${this.preW}px`;
        }else if(this.left < this.scrollW){//如果外层元素的左边距离小于一次滚动的距离那就直接设为0
            this.doc.style.left = '0px';
        }else{
            this.preW=Math.abs(this.left - this.scrollW);//所有滚动元素的宽度减去页面展示的宽度和正常滚动一次的宽度
            this.doc.style.left  = `-${this.preW}px`;  
        }
       
        
       
        
    },
    drag_scroll(e){
        let _this=this
            var e = window.event || e;
            var disX = e.clientX - _this.doc.offsetLeft;
            document.onmousemove=function(e){
                _this.doc.left =( e.clientX - disX) + 'px';
            }
            document.onmouseup=function(e){
                document.οnmοuseup=null;
                document.οnmοusemοve=null;
            }
        
    },
    jumpToDetail(playerNo) {
        let channel = this.getUrlParam("channel") || '';//获取渠道码
        if(channel){
            window.open(this.getOrigin() + this.toUrl + playerNo + "&channel=" + channel);
        }else{
            window.open(this.getOrigin() + this.toUrl + playerNo);
        }
        
    },
    getUrlParam(name) {
        var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)"); //构造一个含有目标参数的正则表达式对象
        var r = window.location.search.substr(1).match(reg); //匹配目标参数
        if (r != null) return decodeURI(r[2]);

        return '';
    },
    getOrigin() {
        let origin = window.location.origin;
        if (!origin) {
            origin = window.location.protocol + "//" + window.location.hostname + (window.location.port ? ':' + window.location.port : '');
        }
        return origin
    }
  },
};
</script>

<style  scoped>
@import "//at.alicdn.com/t/font_1107421_uvtnrezjtb.css";
    .wrap_scroll{
    overflow: hidden;
    width: 100%;
    position: relative;
    height: 208px;
    margin: 20px auto 0;
}
.wrap-scroll_content{
    width: 1152px;
    height: 208px;
    overflow: hidden;
    position: relative;
    margin-left: 24px;
    margin: auto;
}
.wrap-scroll_list{
    position: absolute;
    transition:.5s;
    padding: 0;
    list-style: none;
    
}
li{
        float: left;
        width: 176px;
        margin: 0 8px;
        
    }
   li img{
            cursor: pointer;
        }
.wrap-scroll_btn{
    position: absolute;
    top: 0;
    height: 208px;
    line-height: 208px;
    
}
.iconfont{
        font-size: 20px;
        cursor: pointer;
    }
.scroll-left_btn{
    left: 1px;
}
.scroll-right_btn{
    right: 0;
}
.wrap-scroll_img{
    width: 176px;
    height: 176px;
    border-radius: 100%;
}
</style>
