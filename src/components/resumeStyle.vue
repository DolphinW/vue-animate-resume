<template>
  <div  class="resume-container" >
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
    }
  }
</script>

<style scoped>

</style>
