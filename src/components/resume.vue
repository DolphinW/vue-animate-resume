<template>
  <div>
    <ResumeStyle :code="currentStyleText"></ResumeStyle>
  </div>
</template>

<script>
  import ResumeStyle from './resumeStyle';

  export default {
    name: "resume",
    data(){
      return {
        styleTexts:[
          `/*
          大家好，我是大嘴泡泡家的大脸娃，
          今天给大家讲一个故事，
          大嘴泡泡喜欢吃肉，
          大脸娃娃喜欢吃糖，
          于是我们就一直快乐的在一起啦......
          好了，今天的故事讲完了。
          改改样式，好不好呀~
          */
          /* 代码高亮 */
.token.selector{ color: rgb(123,104,238); }
.token.property{ color: rgb(255,106,106); }
.token.punctuation{ color: green; }
.token.function{ color: rgb(42,161,152); }
          .resume-container{
            transition:all .5s;
            font-size:18px;
            border:1px solid pink;
            width:999px;
            margin:0 auto;
            transform:scale(1.5) rotate(180deg) rotate(-180deg) scale(0.5);
          }
html{
  perspective: 1000px;
}
          `
        ],
        currentStyleText:'',
        interval:100
      }
    },
    created(){
      this.startPrint();
    },
    methods: {
      async startPrint() {
        await this.paintingStyleAndText(0);

      },
      paintingStyleAndText(n){
        return new Promise((resolve,reject)=>{
          let interval=this.interval;
          let paintHtml=(async function(){
              let currentPart=this.styleTexts[n];
              let totalLength=this.styleTexts.filter((style,index)=>index<=n).map(s=>s.length).reduce((sum,item)=>sum+item,0);
              let preLength=totalLength-currentPart.length;
              if(this.currentStyleText.length<totalLength){
                let currentIndex=this.currentStyleText.length-preLength;
                let tmp=currentPart.substring(currentIndex,currentIndex+1);
                this.currentStyleText+=tmp;
                setTimeout(paintHtml,interval);
              }else{
                resolve();
              }
          }).bind(this);
          paintHtml();
        })
      }
    },
    components:{
      ResumeStyle
    }
  }
</script>

<style scoped>

</style>
