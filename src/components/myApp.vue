<template>
    <div v-if="!afterclick" >
      <div id="body">
      <div  v-if="thisIndex < images.length">
        <h2 v-if="thisIndex===0">点击按钮来为图片打分！</h2>
        <h2 v-else-if="thisIndex > 0">你对下列图片的评分是？</h2>
        <img :src="images[thisIndex].url" width="300px" height="500px" style="object-fit: contain;">
        <div>
          <button
            v-for="score in scores"
            :key="score"
            @click="Score(score)" style="margin: 1px; padding: 7px">
            {{ score }}
          </button>
        </div>
      </div>
  
      <div v-else>
        <h2>分析结果！</h2>
      </div>
  
      <div>
        <h2>已打分:</h2>
          <div>
           <div v-for="(image, index) in scoredImg" :key="index">
            <img :src="image.url"  width="80px" height="80px" style="object-fit: cover;" >
            <span>评分: {{ image.score }}</span>
           </div>
          </div>
      </div>
    </div>
    <div id="result" v-if="thisIndex == images.length">
      <div id="resulttext">你的成分是：</div>
      <button id="resultbut" @click="afterclick = !afterclick">点我查看结果</button>
    </div></div>
    <!-- 清空页面后的展示区！ -->
    <div v-if="afterclick" class="chengfen" >
      <div  v-if="average1 == average2 && average3 == average2"><span class="txt">你是：<br>一只狂按按钮的猫 </span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu.JPG" class="mao">
      </div>
      <div  v-else-if="average1 == average2 && average3 < average2 "><span class="txt">你是：<br>无敌赤石大王<br>甘拜下风</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/IMG_1712(20241005-174549).JPG" alt="">
      </div>
      <div  v-else-if="average1 == average2 && average3 > average2 "><span class="txt">你是：<br>正常人</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/IMG_1720.PNG" alt="">
      </div>
      <div  v-else-if="Math.abs(average3 - average2) < 1.7"><span class="txt">你：<br>略微抽象</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/IMG_1721.PNG" alt="">
      </div>
      <div  v-else-if="average1> average2 && average1 > average3"><span class="txt">你是：<br>科比·布莱恩特 </span> 
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu%20(3).JPG" class="kobe">
      </div>
      <div  v-else-if="average2 > average1 && average2 > average3"><span class="txt">你露出鸡脚了 </span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu%20(1).JPG" class="j">
      </div>
      <div  v-else-if="average3 > average1 && average3 > average2"><span class="txt">你也许是：<br>葱粉</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafenrt.png" class="fu">
      </div>


 
      <div  v-else><span class="txt">无法判断成分，你有点奇怪喵</span></div>

    </div>

  

  </template>
  
  <script>
import _ from 'lodash';
import { after } from 'lodash';
  export default {
    data() {
      return {
        images: [
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(1).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(2).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(5).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(3).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(6).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(9).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(4).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(8).JPG' },
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(7).JPG' },
        ],
        thisIndex: 0,
        scoredImg: [],
        scores: [0,1,2,3,4,5,6,7,8,9,10],
        afterclick: false,
      }
    },
    methods: {
      Score(score) {
        this.scoredImg.push({
          url: this.images[this.thisIndex].url,
          score: score
          
        })
        console.log(this.scoredImg)
        this.thisIndex++
      }
    },
    computed:{
      average1(){
        const kobeWeight =[0,10,2,10,2,0,10,0,2]
        const kobes =  _.map(this.scoredImg, (image, index) => image.score * kobeWeight[index]);
        const totalkobes = _.sum(kobes)
        const totalWeight = _.sum(kobeWeight)
        return totalWeight >0 ?totalkobes/totalWeight : 0
      },
      average2(){
        const jWeight =[0,2,10,2,10,0,2,0,10]
        const j =  _.map(this.scoredImg, (image, index) => image.score * jWeight[index]);
        const totalj = _.sum(j)
        const totaljW = _.sum(jWeight)
        return totaljW >0 ?totalj/totaljW : 0
      },
      average3(){
        const fufuWeight =[12,0,0,0,0,12,0,12,0]
        const fufu =  _.map(this.scoredImg, (image, index) => image.score * fufuWeight[index]);
        const totalfufu = _.sum(fufu)
        const totalfufuWeight = _.sum(fufuWeight)
        return totalfufuWeight >0 ?totalfufu/totalfufuWeight : 0
      }
    }
  };
  // console.log(scoredImg)
  </script>
