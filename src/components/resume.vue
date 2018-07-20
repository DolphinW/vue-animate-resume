<template>
  <div>
    <ResumeStyle ref="resumeStyle" :code="currentStyleText"></ResumeStyle>
  </div>
</template>

<script>
  import ResumeStyle from './resumeStyle';

  export default {
    name: "resume",
    data() {
      return {
        styleTexts: [
          `/*
          大家好，我是大嘴泡泡家的大脸娃，
          今天给大家讲一个故事，
          大嘴泡泡喜欢吃肉，
          大脸娃娃喜欢吃糖，
          于是我们就一直快乐的在一起啦......
          好了，今天的故事讲完了。
          变漂亮点儿，好不好呀~
          */

            /* 先准备个 代码高亮 */
            .token.selector{ color: rgb(123,104,238); }
            .token.property{ color: rgb(255,106,106); }
            .token.punctuation{ color: green; }
            .token.function{ color: rgb(42,161,152); }
            /*加个过渡，准备个3d效果基础*/
            html{
              transition:all .5s;
              perspective: 1000px;
            }
            /*白色太单调，来个背景吧*/
            html {
              color: rgb(222,222,222); background:#E6E6FA ;
            }
            .resume-container{
              font-weight:bold;
              font-size:14px;
              border:1px solid pink;
              width:800px;
              transform:rotate(45deg) rotate(-90deg) rotate(45deg);
              transform: rotateY(15deg);
              margin-left:-50px;
              /*最后 背景变得温馨点儿*/
              background:#FFE4E1;
            }
          `
        ],
        currentStyleText: '',
        interval: 40
      }
    },
    created() {
      this.startPrint();
    },
    methods: {
      async startPrint() {
        await this.paintingStyleAndText(0);

      },
      paintingStyleAndText(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval;
          let paintHtml = (async function () {
            let currentPart = this.styleTexts[n];
            let totalLength = this.styleTexts.filter((style, index) => index <= n).map(s => s.length).reduce((sum, item) => sum + item, 0);
            let preLength = totalLength - currentPart.length;
            if (this.currentStyleText.length < totalLength) {
              let currentIndex = this.currentStyleText.length - preLength;
              let tmp = currentPart.substring(currentIndex, currentIndex + 1);
              this.currentStyleText += tmp;
              // if (currentPart.substring(currentIndex - 1,currentIndex ) === '\n' && this.$refs.resumeStyle) {
              //   this.$nextTick(() => {
              //     this.$refs.resumeStyle.goBottom()
              //   })
              // }
              setTimeout(paintHtml, interval);
            } else {
              resolve();
            }
          }).bind(this);
          paintHtml();
        })
      }
    },
    components: {
      ResumeStyle
    }
  }
</script>

<style scoped>

</style>
