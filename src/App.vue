<template>
  <div id="app">
    <h1>在线翻译</h1>
    <h5 class="text-muted">简单 / 易用 / 便捷 /</h5>
    <translateForm v-on:formSubmit="translateText"></translateForm>
    <translateOutput v-text="translatedText"></translateOutput>
  </div>
</template>

<script>
import translateForm from './components/translateForm'
import translateOutput from './components/translateOutput'

export default {
  name: 'app',
  data: function() {
    return  {
      translatedText: ''
    }
  },
  components: {
    translateForm,translateOutput
  },
  methods: {
    translateText: function (text,language) {
      // alert(language);
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20171006T011915Z.793d1bd8153dd056.593527c01d77129fbc43215cf208441d530e5049&lang='+language+'&text='+text)
          .then((response)=>{
            // console.log(response.body.text[0]);
            this.translatedText = response.body.text[0];
          })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
