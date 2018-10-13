<template>
  <div id="app">
    <fieldset>
      <legend>Vue Translator</legend>

      <div class="input-field">
        <label></label>
        <input class="inText" type="text" v-model="input" placeholder="Type to translate..">
      </div>

      

      <div class="container">
        <div class="row">
          
              <button type="button"  class="button-info lang-btn" v-model="language" @click="language='es'">Spanish</button> 
         
              <button type="button" class="button-info lang-btn" v-model="language" @click="language='ru'">Russian</button> 
          
              <button type="button" class="button-info lang-btn" v-model="language" @click="language='fr'">French</button> 
          
              <button type="button" class="button-info lang-btn" v-model="language" @click="language='zh'">Chinese</button> 
          
              <button type="button" class="button-info lang-btn" v-model="language" @click="language='mn'">Mongolian</button> 
          
              <button type="button" class="button-info lang-btn" v-model="language" @click="language='de'">German</button> 
              
        </div>

        
</div>

      

      <div class="input-field">
        <label>Result</label>
        <textarea class="inText" v-model="answer"></textarea>
      </div>

    </fieldset>
  </div>
</template>

<script>
export default {

  data(){
    return {
      input: '',
      answer: '',
      language: 'es',
      key:  'trnsl.1.1.20170329T180255Z.3c18d2dc7b65d525.f23ed9a9efa992bded4ef96334e3c154f61d2dea' 
    }
  },
  watch: {
    input: function() {
      this.answer = 'Waiting for you to stop typing...'
      this.getAnswer()
    },
    language: function() {
      this.getAnswer()
    }
  },
  methods: {
    getAnswer: _.debounce(
      function() {
        this.answer = 'Thinking...';
        var vm = this;
        axios.get(`https://translate.yandex.net/api/v1.5/tr.json/translate?key=${this.key}&lang=${this.language}&text=${this.input}`)
          .then(function(response) {
            vm.answer = "Translation: " + _.capitalize(response.data.text)
          })
      },500)
  }

}
</script>


<style>

.lang-btn{
    display: inline-block;
    margin: 5px;
  
}

  body{
    display: flex;
    min-height: 100vh;
    justify-content: center;
    align-items: center;
  }

  div {
    max-width: 768px;
    width: 100%;
  }

  input {
    margin-bottom: 3rem;
  }

  body{
    background-image: url('./assets/DSC03487-Edit-min.jpg');
    background-repeat:no-repeat;
    background-size:contain;
    background-position:center; 
    background-color: black;
  }

  legend{
    color: white;
  }

  .input-field{
    color: white;
  }

</style>
