<template>

      <div id="body" class="unselectable">
      <div  v-if="thisIndex < randomImages.length">
        <h2 v-if="thisIndex===0" >这是一个用来测试成分的打分小网站！<br>点击按钮来为图片打分--></h2>
        <h2 v-else-if="thisIndex > 0">你对下列图片的评分是？</h2>
        <img :src="randomImages[thisIndex].url" width="90%" height="800px" style="object-fit: contain;">
        <div>
          <button
            v-for="score in scores"
            :key="score"
            @click="Score(score)" style="margin: 1px; padding: 7px ;position: relative;" class="but" >
            {{ score }}
          </button>
        </div>
      </div>
  
      <div v-else>
        <h2 class="unselectable">全部完成！分析结果--></h2>
      </div>
  
      <div>
        <h2>已打分:</h2>
          <div>
           <div v-for="(image, index) in scoredImg" :key="index" style="display: inline-block;margin: 20px;" class="unselectable">
            <img :src="image.url"   style="object-fit: cover; width:80px; height:80px" >
            <span style="font-weight: bold;" class="unselectable">评分: {{ image.score }}</span>
           </div>
          </div>
      </div>
    </div>
    <div id="result" v-if="thisIndex == randomImages.length">
      
      <button id="resultbut" class="unselectable" @click="afterclick = !afterclick"><span v-if="!afterclick">点我查看分析结果</span><br><span v-if="afterclick" style="font-size: 15px;opacity: .6;">(鼠标选中下方卡片)</span></button>
    </div>
    
    <!-- 清空页面后的展示区！ -->
    <div v-if="afterclick" class="chengfen" >
    
      <!-- <div  v-if="average1 == average2 && average3 == average2"><span class="txt">你是：<br>一只狂按按钮的猫 </span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu.JPG" class="mao">
      </div>
      <div  v-else-if="average1 == average2 && average3 < average2 "><span class="txt">你是：<br>无敌赤石大王<br>甘拜下风</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/IMG_1712(20241005-174549).JPG" alt="">
      </div>
      <div  v-else-if="average1 == average2 && average3 > average2 "><span class="txt">没准你是：<br>正常人</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/IMG_1720.PNG" alt="">
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
      <div  v-else-if="1.6 < Math.abs(average3 - average2) < 1.69 || 1.6 < Math.abs(average3 - average1) < 1.69"><span class="txt">你：<br>略微抽象</span>
        <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/IMG_1721.PNG" alt="">
      </div>
      <div  v-else><span class="txt">无法判断成分，你有点奇怪喵</span></div> -->
      <div v-if="first" style="width: 100%;position: relative;">

          <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu.JPG" class="mao" style="width: 80%;">
        <h2  class="ifh2"> 你分明没有认真评分嘛！</h2>
      </div>
      <div v-else class="cont">
        <div class="container">
          <div class="card unselectable" style="--i:-3;"> 
            <img v-if="erciyuan >= 85" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/miumiu%20(2).PNG"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">
            <img v-else-if="erciyuan >= 50 && erciyuan <85" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/miumiu%20(1).PNG"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">
            <img v-else-if="erciyuan <50" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/miumiu%20(3).PNG" class="mao" style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">

            <h2 style="font-size: 2rem; width: 100%;position: relative;text-align: center;color: pink;" class="cardTitle">
              你的二次元指数是
              <h1 v-if="erciyuan >= 50 && erciyuan <85" style="color: yellowgreen;">{{ erciyuan.toFixed(0) }}</h1>
              <h1 v-else-if="erciyuan >= 85" style="color: rebeccapurple;">{{ erciyuan.toFixed(0) }}</h1>
              <h1 v-else style="color: yellow;">{{ erciyuan.toFixed(0) }}</h1>

            </h2>
            <h3 v-if="erciyuan >= 85" style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;text-shadow: 0 0 0px #000;">
              我去，<br>铁血二次元</h3>

            <h3 v-if="erciyuan >= 50 && erciyuan <85" style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;text-shadow: 0 0 5px #000;color: #c1ebff;">
              核验通过<br>你应该是正常人！(^_^)</h3>

            <h3 v-if="erciyuan <50" style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;text-shadow: 0 0 20px #000;color: white;">
             牢底,<br>你的审美包有问题<br></h3>

          </div>


          <div class="card unselectable" style="--i:-2;"> 
            <img v-if="chouxiang >= 85" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(5).JPG"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">
            <img v-else-if="chouxiang >= 50 && chouxiang <85" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang2.JPG"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">
            <img v-else-if="chouxiang <50" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang3.JPG" class="mao" style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">

            <h2 style="font-size: 2rem; width: 100%;position: relative;text-align: center;color: blueviolet;" class="cardTitle">
              你的抽象指数是
              <h1>{{ chouxiang.toFixed(1) }}</h1>
            </h2>
            <h3 v-if="chouxiang >= 85" style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;text-shadow: 0 0px 20px #000;color: aliceblue;">
              难评<br>请打开tab输入<br>/remake</h3>

            <h3 v-if="chouxiang >= 50 && chouxiang <85" style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;text-shadow: 0 0 20px #000;color: yellow;">
              都正常点<br>正常点好啊</h3>

            <h3 v-if="chouxiang <50" style="position: absolute;top: 80%;margin: 2px;padding: 2px;text-align: center;text-shadow: 0 0 20px #000;color: aliceblue;">
             很好！<br>继续保持！<br></h3>
          </div>


          <div class="card unselectable" style="--i:-1;"> 
            <h2 v-if="tiyu<=70" style="font-size: 2rem; width: 100%;position: relative;color: white;text-align: center;" class="sTitle">
                    <h2 style="position: absolute;top: -10%;font-size: 35px;">你不怎么关注体育明星</h2>
                    <h2 v-if="laoda >=90" id="laoda">
                      <h2 style="z-index: 1;font-size: 20px;position: absolute;bottom: 0%;text-align: center;">但你肯定是牢大忠粉</h2>
                      <img src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/laoda.JPG" alt="" style="object-fit: contain;width: 100%;position: absolute;bottom: 0;left: 0;z-index: -1;">

                    </h2>
            </h2>
            <h2 v-else style="font-size: 2rem; width: 100%;position: relative;text-align: center;color: white;" class="sTitle">
                    <h2 style="font-size: 1.6rem;">你给体育明星们都打了高分，也许你热衷于体育赛事</h2>
                    <h2 v-if="laoda >=90" id="laoda">
                      <h2 style="z-index: 1;font-size: 20px;position: absolute;bottom: 0;;text-align: center;">当然，你一定是牢大忠粉</h2>
                      <img src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/laoda666.JPG" alt="" style="object-fit: contain;width: 100%;position: absolute;bottom: 0;left: 0;z-index: -1;">

                    </h2>
            </h2>
          </div>


          <div class="card unselectable" style="--i:0;">
            <h2 v-if="yule<=70" style="font-size: 2rem; width: 100%;position: relative;color: white;text-align: center;" class="sTitle">
              <h2 style="font-size: 1.6rem;">不混娱乐圈是好文明</h2>

              <h2 v-if="ji >=80" class="ji">

                      <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu%20(1).JPG" style="position: absolute;bottom: 0;width: 240px;left: 0;z-index: -1;">

                    </h2>
                    <h2 v-else  class="ji" style="height: 80%;">
                      <h2 style="font-size: 30px;bottom: 0%;opacity: 0.7;"></h2>
                      <img src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/jige.JPG" style="position: absolute;bottom: 0;width: 240px;left: 0;z-index: -1;">
                    </h2>
            </h2>
            <h2 v-else style="font-size: 2rem; width: 100%;position: relative;text-align: center;color: white" class="sTitle">
                    <h2 style="font-size: 1.6rem;">可以混圈，不要过度</h2>
                    <h2 v-if="ji >=80" class="ji">

                      <img src="https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafentu%20(1).JPG" style="position: absolute;bottom: 0;width: 240px;left: 0;z-index: -1;">

                    </h2>
                    <h2 v-else  class="ji" style="height: 80%;">
                      <h2 style="font-size: 30px;bottom: 0%;opacity: 0.7;"></h2>
                      <img src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/jige.JPG" style="position: absolute;bottom: 0;width: 240px;left: 0;z-index: -1;">
                    </h2>
            </h2>
          </div>


          <div class="card unselectable" style="--i:1;">
            <img v-if="mao <= 50" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/maomaomao.jpg"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">

            <h2 style="font-size: 2rem; width: 100%;position: relative;text-align: center;color: yellow;" class="cardTitle">
              你的猫猫指数是
              <h1 v-if="mao<=50" style="font-size: 35px;color: orange;">{{ mao.toFixed(1) }}</h1>
              <h1 v-else>{{ mao.toFixed(1) }}</h1>
            </h2>
            <h2 v-if="mao<=50" style="font-size: 2rem; width: 100%;position: absolute;color: red;bottom: 0;font-size: 1.5rem;" id="mao">
              补药昧着良心给猫猫打低分啊（恼火）
            </h2>

          </div>


          <div class="card unselectable" style="--i:2;" id="v">
            <img v-if="v >= 80" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/vquandashouzi.JPG"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">
            <img v-if="v < 80" src="https://vue-1329849192.cos.ap-chengdu.myqcloud.com/jianglini.JPG"  style="width: 100%;height: 100%;object-fit:cover ;position: absolute;bottom: 0;">
            <h2 v-if="v>=80" style="font-size: 2rem; width: 100%;position: relative;text-align: center;text-shadow:0 0 20px #000;" class="cardTitle">
              你好像是<br>V圈大手子
            <h1  style="font-size: 35px;color: blue;">这辈子有了</h1>
          </h2>
          <h2 v-if="v<80" style="font-size: 2rem; width: 100%;position: relative;text-align: center;text-shadow:0 0 20px #000;" class="cardTitle">
              不喜欢皮套人？
            <h1  style="font-size: 35px;color: sandybrown;">好好好！奖励你一个西瓜</h1>
          </h2>
          </div>

          <div v-if="all >= 75" class="card unselectable" style="--i:3; background:linear-gradient(270deg,orange,yellow,orange ) ;background-size: 200%; animation: flow 5s linear infinite;" > 
            <h2 style="font-size: 2rem; width: 100%;position: relative;text-align: center;" class="cardTitle">
              你对所有图片的评价均分是
              <h1>{{ all.toFixed(1) }}</h1>
            </h2>

            <h3  style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;">
              你的打分十分慷慨<br>一定是个很温柔的人吧！</h3>


          </div>
          <div v-else-if="all >= 50 && all <75" class="card unselectable" style="--i:3; background:linear-gradient(270deg,#c1ebff,#55daf8,#c1ebff ) ;background-size: 200%; animation: flow 5s linear infinite;" > 
            <h2 style="font-size: 2rem; width: 100%;position: relative;text-align: center;" class="cardTitle">
              你对所有图片的评价均分是
              <h1>{{ all.toFixed(1) }}</h1>
            </h2>

            <h3  style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;">
              公正客观<br>人民评论家</h3>

          </div>
          <div v-else-if="all <50" class="card unselectable" style="--i:3; background:linear-gradient(270deg,#ff0000,#fff,#ff0000 ) ;background-size: 200%; animation: flow 5s linear infinite;" > 
            <h2 style="font-size: 2rem; width: 100%;position: relative;text-align: center;" class="cardTitle">
              你对所有图片的评价均分是
              <h1>{{ all.toFixed(1) }}</h1>
            </h2>
            <h3  style="position: absolute;top: 70%;margin: 2px;padding: 2px;text-align: center;">
              你有点苛刻了<br>一张喜欢的都没有吗qwq</h3>

          </div>

        </div>
      </div>






      <div id="result">

      <button id="resultbut2" class="unselectable" @click="refresh()" style="color: yellow;">点我重新开始测试！</button>
      </div>



    </div>
    <div class="end">被你发现了！<a href="https://drtonks.github.io/myblog.github.io/" target="_blank">那就收藏一下我的博客再走吧！</a></div>
  </template>
  
  <script>
import _ from 'lodash';
import { after } from 'lodash';
  export default {
    data() {
      return {
        
        images: [
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(1).JPG' ,tag:['erciyuan','fufu']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(2).JPG' ,tag:['tiyu','laoda','chouxiang']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(5).JPG' ,tag:['yule','ji']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(3).JPG' ,tag:['tiyu','laoda','chouxiang']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(6).JPG' ,tag:['yule','ji','chouxiang']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(9).JPG' ,tag:['erciyuan','fufu']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(4).JPG' ,tag:['tiyu','laoda']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(8).JPG' ,tag:['erciyuan','fufu']},
          { url: 'https://tonks-blog-1329849192.cos.ap-chengdu.myqcloud.com/dafen%20(7).JPG' ,tag:['yule','ji']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/erciyuan%20(1).JPG',tag:['erciyuan']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/erciyuan%20(1).PNG',tag:['erciyuan']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/erciyuan%20(2).PNG',tag:['erciyuan']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/erciyuan%20(3).PNG',tag:['erciyuan']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/erciyuan%20(4).PNG',tag:['erciyuan']},

          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/tiyu%20(1).JPG',tag:['tiyu']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/tiyu%20(2).JPG',tag:['tiyu']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/tiyu%20(3).JPG',tag:['tiyu']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/tiyu%20(4).JPG',tag:['tiyu']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/tiyu%20(5).JPG',tag:['tiyu']},

          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/yule%20(1).JPG',tag:['yule']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/yule%20(2).JPG',tag:['yule']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/yule%20(3).JPG',tag:['yule']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/yule%20(4).JPG',tag:['yule']},
          { url: 'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/yule%20(5).JPG',tag:['yule']},

          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/maomao%20(1).JPG',tag:['mao']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/maomao%20(2).JPG',tag:['mao']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/maomao%20(3).JPG',tag:['mao']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/maomao%20(4).JPG',tag:['mao']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/maomao%20(5).JPG',tag:['mao']},

          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang%20(1).JPG',tag:['chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang%20(2).JPG',tag:['chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang%20(3).JPG',tag:['chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang%20(4).JPG',tag:['chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/chouxiang%20(5).JPG',tag:['chouxiang']},


          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(1).JPG',tag:['v','chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(2).JPG',tag:['v','chouxiang','erciyuan']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(3).JPG',tag:['v','chouxiang','erciyuan']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(4).JPG',tag:['v','chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(5).JPG',tag:['v','chouxiang']},
          { url:'https://vue-1329849192.cos.ap-chengdu.myqcloud.com/v%20(6).JPG',tag:['v','erciyuan']},

        ],
        // isBackgroundBlack: false,
        thisIndex: 0,
        scoredImg: [],
        randomImages:[],
        scores: [0,1,2,3,4,5,6,7,8,9,10],
        afterclick: false,
        erciyuan:[],
        tiyu:[],
        yule:[],
        fufu:[],
        ji:[],
        laoda:[],
        chouxiang:[],
        v:[],
        mao:[],
      }
    },
    mounted() {
    this.getRandomImages(); //组件加载时获取
  },
    methods: {
      // afterclick() {
      // this.isBackgroundBlack = !this.isBackgroundBlack; // 切换背景状态
      // document.body.style.backgroundColor = this.isBackgroundBlack ? 'black' : 'white'; // 设置背景颜色
      // console.log('isBackgroundBlack:', this.isBackgroundBlack); 
      // },
      refresh(){
        window.location.reload();
      },
      getRandomImages(){
        const shuffledImages = _.shuffle(this.images); // 打乱
      this.randomImages = shuffledImages.slice(0, 30); // 选择随机图片
      },
      Score(score) {
        const currentImage = this.randomImages[this.thisIndex];
        this.scoredImg.push({
          url: this.randomImages[this.thisIndex].url,
          score: score
        
        });
      if (currentImage.tag.includes('erciyuan')) {
        this.erciyuan.push({
          url: currentImage.url,
          score: score,
        });
        console.log('二次元分数:', this.erciyuan); 
      }
      if (currentImage.tag.includes('tiyu')) {
        this.tiyu.push({
          url: currentImage.url,
          score: score,
        });
        console.log('体育人物分数:', this.tiyu); 
      }
      if (currentImage.tag.includes('yule')) {
        this.yule.push({
          url: currentImage.url,
          score: score,
        });
        console.log('娱乐明星分数:', this.yule);
      }
      if (currentImage.tag.includes('fufu')) {
        this.fufu.push({
          url: currentImage.url,
          score: score,
        });
        console.log('fufu分数:', this.fufu);
      }
      if (currentImage.tag.includes('laoda')) {
        this.laoda.push({
          url: currentImage.url,
          score: score,
        });
        console.log('老大分数:', this.laoda);
      }
      if (currentImage.tag.includes('ji')) {
        this.ji.push({
          url: currentImage.url,
          score: score,
        });
        console.log('蔡徐坤分数:', this.ji);
      }
      if (currentImage.tag.includes('chouxiang')) {
        this.chouxiang.push({
          url: currentImage.url,
          score: score,
        });

      }
      if (currentImage.tag.includes('v')) {
        this.v.push({
          url: currentImage.url,
          score: score,
        });

      } 
      if (currentImage.tag.includes('mao')) {
        this.mao.push({
          url: currentImage.url,
          score: score,
        });

      }
        this.thisIndex++;

      },

    },
    
computed: {

  first(){
    // 只提取评分
    const count1 = this.scoredImg.map(item => item.score);
    const arr = [...count1];
    // 去重
    const result = [...new Set(arr)];  //直接使用set,同四题
    return result.length === 1;  // 检查去重后的数组是否只有一个元素
  },
  erciyuan(){
    const erciyuan=this.erciyuan.map(item => item.score)
    const erciyuanSum=_.sum(erciyuan)
    const average = 10*erciyuanSum/erciyuan.length
    return average
  },
  tiyu(){
    if(this.tiyu.length){

    const tiyu=this.tiyu.map(item => item.score)
    const Sum=_.sum(tiyu)
    const average = 10*Sum/tiyu.length
    return average}
    else{
      return 0;
    }
  },
  yule(){
    if(this.yule.length){
    const yule=this.yule.map(item => item.score)
    const Sum=_.sum(yule)
    const average = 10*Sum/yule.length
    return average}
    else{
      return 0;
    }
  },
  v(){
    if(this.v.length){
    const all=this.v.map(item => item.score)
    const Sum=_.sum(all)
    const average = 10*Sum/all.length
    return average}
    else{
      return 0;
    }
  },
  chouxiang(){
    if(this.chouxiang.length){
    const all=this.chouxiang.map(item => item.score)
    const Sum=_.sum(all)
    const average = 10*Sum/all.length
    return average}
    else{
      return 0;
    }
  },
  mao(){
    if(this.mao.length){
    const all=this.mao.map(item => item.score)
    const Sum=_.sum(all)
    const average = 10*Sum/all.length
    return average}
    else{
      return 0;
    }
  },

  laoda(){
    if(this.laoda.length){
    const laoda=this.laoda.map(item => item.score)
    const Sum=_.sum(laoda)
    const average = 10*Sum/laoda.length
    return average}
    else{
      return 0;
    }
  },
  ji(){
    if(this.ji.length){

    const ji=this.ji.map(item => item.score)
    const Sum=_.sum(ji)
    const average = 10*Sum/ji.length
    return average}
    else{
      return 0;
    }
  },
  fufu(){
    if(this.fufu.length){
    const fufu=this.chuyin.map(item => item.score)
    const Sum=_.sum(fufu)
    const average = 10*Sum/fufu.length
    return average}
    else{
      return 0;
    }
  },

  all(){
    const all = this.scoredImg.map(item => item.score)
    const Sum =_.sum(all)
    return Sum*10/all.length
  }
}

  };
  // console.log(scoredImg)
  </script>
