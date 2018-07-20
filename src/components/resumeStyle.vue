<template>
  <div  class="resume-container" ref="container">
    <div v-html="textStyleContainer"></div>
    <pre v-html="styleText"></pre>
  </div>
</template>

<script>
  import Prism from 'prismjs';

  export default {
    name: "resume-style",
    props:{
      code:{
        type:String,
        default:''
      }
    },
    computed:{
      textStyleContainer(){
        return `<style>${this.code}</style>`
      },
      styleText(){
        return Prism.highlight(this.code, Prism.languages.css);
      }
    },
    methods: {
      goBottom() {
        this.$refs.container.scrollTop = 100000
      }
    },
  }
</script>

<style scoped>

</style>
