<template>
  <div id="Photo" @mousemove="move" @mouseenter="enter" @mouseleave="leave">
      <div class="view">
          <div class="box1">
              <ul class="ul" id="viweLi">
                <li><img src="../../static/img/bg1.jpg" alt="图片加载失败"></li>
                <li><img src='../../static/img/bg2.jpg' alt="图片加载失败"></li>
                <li><img src='../../static/img/bg3.jpg' alt="图片加载失败"></li>
              </ul>
          </div>
      </div>
      <div class="left">
          <div class="box2">
            <ul class="ul" id="leftLi">
                <li><div class="empty"></div></li>
                <li><img src='../../static/img/bg1.jpg' alt="图片加载失败"></li>
                <li><img src='../../static/img/bg2.jpg' alt="图片加载失败"></li>
            </ul>
          </div>
      </div>
      <div class="right">
          <div class="box3">
              <ul class="ul" id="rightLi">
                  <li><img src='../../static/img/bg2.jpg' alt="图片加载失败"></li>
                  <li><img src='../../static/img/bg3.jpg' alt="图片加载失败"></li>
                  <li><div class="empty"></div></li>
              </ul>
          </div>
      </div>
  </div>
</template>
<script>
export default {
  name: 'Photo',
  data(){
      return {
          leftLen:0,
          clientWidth:0,
          EnterpointX:0,
          speed:20
      }
  },
  mounted(){
        let Cwidth;
        let childrenlen=window.document.getElementsByClassName('ul')[0]?window.document.getElementsByClassName('ul')[0].children.length:0;
        //总长度用于判断是否滑到底
        if(childrenlen)Cwidth=window.document.getElementsByClassName('ul')[0].children[0].clientWidth;
        this.leftLen=childrenlen*Cwidth;
        this.clientWidth=Cwidth;
        console.log(this.leftLen);
  },
  methods:{
      move(el){
          //右边
          if(el.screenX>this.EnterpointX){
              this.EnterpointX=el.screenX;
              if(Math.abs(window.document.getElementById('viweLi').offsetLeft)>=(Math.abs(this.leftLen)-this.clientWidth))return;
              window.document.getElementById('viweLi').style.left=`${window.document.getElementById('viweLi').offsetLeft-this.speed}px`;
              window.document.getElementById('leftLi').style.left=`${window.document.getElementById('leftLi').offsetLeft-this.speed}px`;
              window.document.getElementById('rightLi').style.left=`${window.document.getElementById('rightLi').offsetLeft-this.speed}px`;
          }else{
              this.EnterpointX=el.screenX;
              if(window.document.getElementById('viweLi').offsetLeft>=0)return;
              window.document.getElementById('viweLi').style.left=`${window.document.getElementById('viweLi').offsetLeft+this.speed}px`;
              window.document.getElementById('leftLi').style.left=`${window.document.getElementById('leftLi').offsetLeft+this.speed}px`;
              window.document.getElementById('rightLi').style.left=`${window.document.getElementById('rightLi').offsetLeft+this.speed}px`;
          }
      },
      enter(el){
          this.EnterpointX=el.screenX;
      },
      leave(el){
          this.EnterpointX=el.screenX;
      },
      Iconmove(Icon){
          for(let i=0;i<Icon.length;i++){
              Icon[i].style.left=`100px`;
          }

      }
  }
}
</script>
<style scoped>
#Photo {
    position: absolute;
    height: 920px;
    width: 100%;
    background-color: #2e2d31;
    transform-style: preserve-3d;
    perspective: 600px;
    overflow: hidden;
}
.view{
    position: absolute;
    background-color: aliceblue;
    height: 600px;
    width: 895px;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%) translateZ(135px);
    overflow: hidden;
}
.left{
    position: absolute;
    height: 600px;
    width: 895px;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%) rotateY(90deg) translate3d(-582px,0px,-448px);
    overflow: hidden;
}
.right{
    position: absolute;
    height: 600px;
    width: 895px;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%) rotateY(-90deg) translate3d(582px,0px,-448px);
    overflow: hidden;
}
img{
    height: 600px;
    width: 895px;
    object-fit:cover;
}
.box1,.box2,.box3{
    height: 600px;
    width: 895px;
}
ul{
    position: absolute;
    white-space: nowrap;
}
ul li{
    display:inline-block;
    font-size: 0;
    height: 600px;
    width: 895px;
}
</style>