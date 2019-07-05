<template>
  <div id="app">
    <form action="#" method="post">
      <DragDrop name="uploadfile" multiple="multiple" @checkResult="getResult"/>

      <button id="btnSubmit" v-bind:disabled="checkDisabled">送信する</button>
    </form>

    <div id="resultFile"></div>
  </div>
</template>

<script>
import DragDrop from './components/DragDrop.vue'

export default {
  name: 'app',
  components: {
    DragDrop
  },
  data () {
    return {
      checkDisabled: true
    }
  },
  methods: {
    getResult(result){
      // -----------------------
      // この中は自由に処理してください
      // -----------------------
      // とりあえずファイル選択したFile情報を返している
      // エラーの時はnull

      let resultTxt = '';

      console.log(result);
      Array.from(result).forEach((elm)=>{
        resultTxt += 'File Name : ' + elm.name + '\n';
      });

      document.getElementById('resultFile').innerText = resultTxt;

      if(result) {
        this.checkDisabled = false;
      }
      else {
        this.checkDisabled = true;
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  padding: 100px;
}

#resultFile {
  margin-top: 100px;
  line-height: 2;
}

#btnSubmit {
  display: block;
  margin-top: 50px;
  border: 1px solid #000;
  border-radius: 10px;
  padding: 20px;
  cursor: pointer;

  &:disabled {
    background-color: #999;
    cursor: not-allowed;
  }
}
</style>
