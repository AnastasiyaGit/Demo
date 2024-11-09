<template>
<div v-if="userAgent" id="main">
<img id="img" ref="imgRef" src="../public/media/Background.png">
<!--  левый вертикальный ряд - 1 вертикальный ряд-->
<img id="img1" class="sample left1 top1" src="../public/media/1.png" @click="setInfo('img1')">
<img id="img2" class="sample left1 top2" src="../public/media/1.png" @click="setInfo('img2')">
<img id="img3" class="sample left1 top3" src="../public/media/1.png" @click="setInfo('img3')">
  <!--  2 вертикальный ряд-->
<img id="img4" class="sample left2 top1" src="../public/media/1.png" @click="setInfo('img4')">
<img id="img5" class="sample left2 top2" src="../public/media/1.png" @click="setInfo('img5')">
  <!--  3 вертикальный ряд-->
<img id="img6" class="sample left3 top1" src="../public/media/1.png" @click="setInfo('img6')">
<img id="img7" class="sample left3 top2" src="../public/media/1.png" @click="setInfo('img7')">
  <!--  левый вертикальный ряд - 1 вертикальный ряд-->
<img id="img8" class="sample left4 top1" src="../public/media/1.png" @click="setInfo('img8')">
<img id="img9" class="sample left4 top2" src="../public/media/1.png" @click="setInfo('img9')">
<img id="img10" class="sample left4 top3" src="../public/media/1.png" @click="setInfo('img10')">
<!--  screen-->
  <div id="screen" class="left-screen top-screen"><a :href="link" target="_self">{{info}}</a></div>
</div>
  <div v-else id="no-main">
    <h1>SORRY</h1>
    <h2>NO ACCESS</h2>
  </div>
</template>

<script setup>
import {nextTick, onMounted, onUpdated, ref} from "vue";

const userAgent = ref(false)

const imgRef = ref()

const imgWidth = ref(0)
const imgHeight = ref(0)

const leftOffset = ref()
const topOffset = ref()

const windowInnerWidth = window.innerWidth
const windowInnerHeight = window.innerHeight

const mainArray = ref([
  {id:'img1',info:'dgdgd gdfgdfg gdfgdh gdfhdhd',link:'https://www.tek.com/en'},
  {id:'img2',info:'gdfhfg h htfh',link:'https://www.tek.com/en'},
  {id:'img3',info:'hdfbb j jfjd',link:'https://www.tek.com/en'},
  {id:'img4',info:'hjfgj n h',link:'https://www.tek.com/en'},
  {id:'img5',info:'jghjghmgh  mghghjg',link:'https://www.tek.com/en'},
  {id:'img6',info:'jghjn jghj',link:'https://www.tek.com/en'},
  {id:'img7',info:'gjhghnjgnjg',link:'https://www.tek.com/en'},
  {id:'img8',info:'jghjghkh mghkghjg  jgh',link:'https://www.tek.com/en'},
  {id:'img9',info:'jkghkj jghjg',link:'https://www.tek.com/en'},
  {id:'img10',info:'jghjkn jghj jgh',link:'https://www.tek.com/en'},
])
const info = ref()
const link = ref()
const setInfo = (id)=>{
  let sample = document.getElementsByClassName('sample')
  Array.from(sample).forEach((item) => {
    item.classList.remove('active')
  });
  let currentImg = document.getElementById(id)
  currentImg.classList.add('active')
  let el = mainArray.value.find(item=>{return item.id===id})
  info.value = el.info
  link.value = el.link
}
const getImageWidthHeight = () => {
  if (imgRef.value) {
    imgWidth.value = imgRef.value.clientWidth;
    imgHeight.value = imgRef.value.clientHeight;
    leftOffset.value = (windowInnerWidth - imgWidth.value)/2
    topOffset.value = (windowInnerHeight - imgHeight.value)/2
  }
};
const setSample = ()=>{
  let sample = document.getElementsByClassName('sample')
  let left1 = document.getElementsByClassName('left1')
  let left2 = document.getElementsByClassName('left2')
  let left3 = document.getElementsByClassName('left3')
  let left4 = document.getElementsByClassName('left4')
  let top1 = document.getElementsByClassName('top1')
  let top2 = document.getElementsByClassName('top2')
  let top3 = document.getElementsByClassName('top3')
  Array.from(sample).forEach((item) => {
    item.style.width =  (13.0/174)*imgWidth.value + 'px'// пропорции компа
  });
  Array.from(left1).forEach((item) => {
    item.style.left = leftOffset.value+(13.0/174)*imgWidth.value + 'px'// пропорции компа
  });
  Array.from(left2).forEach((item) => {
    item.style.left = leftOffset.value+(33.0/174)*imgWidth.value + 'px'// пропорции компа
  });
  Array.from(left3).forEach((item) => {
    item.style.left = leftOffset.value+(132.0/174)*imgWidth.value + 'px'// пропорции компа
  });
  Array.from(left4).forEach((item) => {
    item.style.left = leftOffset.value+(152.0/174)*imgWidth.value + 'px'// пропорции компа
  });
  Array.from(top1).forEach((item) => {
    item.style.top = topOffset.value+(27.0/162)*imgHeight.value + 'px'// пропорции 16 айфона
  });
  Array.from(top2).forEach((item) => {
    item.style.top = topOffset.value+(50.0/162)*imgHeight.value + 'px'// пропорции 16 айфона
  });
  Array.from(top3).forEach((item) => {
    item.style.top = topOffset.value+(73.0/162)*imgHeight.value + 'px'// пропорции 16 айфона
  });
}
const setScreen = ()=>{
  let screen = document.getElementById('screen')
  screen.style.width =  (72.0/174)*imgWidth.value + 'px'// пропорции компа
  screen.style.height =  (40.0/260)*imgHeight.value + 'px'// пропорции компа

  screen.style.left = leftOffset.value+(51.0/174)*imgWidth.value + 'px'// пропорции компа
  screen.style.top = topOffset.value+(73.0/162)*imgHeight.value + 'px'// пропорции 16 айфона
}
onMounted( async ()=>{
  const width = window.screen.width;
  const height = window.screen.height;
  console.log(width)
  console.log(height)
  if(+width === 393 && +height === 852){
    userAgent.value = true
  }
  else{
    userAgent.value = false
    return
  }


  await nextTick(()=>{
    let img = document.getElementById('img')
    if(windowInnerWidth<=windowInnerHeight){
      img.style.width='100%'
      img.style.height='auto'
    }
    else{
      img.style.width='auto'
      img.style.height='100vh'
    }
    if (imgRef.value.complete) {
      getImageWidthHeight()
      setSample()
      setScreen()
    } else {
      img.addEventListener('load',function () {
        getImageWidthHeight()
        setSample()
        setScreen()
      });
    }
  })

})

</script>

<style scoped lang="scss">
#main{
  font-size: 10px;
  display: flex;
  height: 100vh;
  background-color: #b0b0b0;
  img {
    display: block;
    margin:auto;
    vertical-align: middle;
  }
  .sample{
    position: absolute;
  }
  .active{
    border: 1px solid #73bf44;
    box-shadow: 0 1px 3px 3px #73bf44;
  }
  #screen{
    position: absolute;
    color:#fff;
    align-content: center;
    text-align: center;
    font-size: 1rem;
    a{
      text-decoration: none;
      color:#fff;
    }
  }

}
#no-main{
  height: 100vh;
  align-content: center;
  text-align: center;
}
</style>
