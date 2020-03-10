<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :total="total" />
    <b-container class="bv-example-row">
  <b-row>
    <b-col sm="6" offset="3">
    <QuestionBox v-if="Questions.length > 0" :currentQuestion="Questions[index]"   :increament="increament" v-bind:next="next"/>
    </b-col>
  </b-row>
</b-container>
  
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },

  data(){
    return{
    Questions:[],
    index:0,
    numCorrect:0,
    total:0,
    }
  } ,
  methods:{
        next(){
          this.index++
        },
        increament(isCorrect){
          if(isCorrect==true){
            this.numCorrect++
            this.total++
          }
          else{
            this.total++
          }
 
        }
  }
  ,

  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=9',{method:'get'}).then((response)=>{
    return response.json()
  }).then((jsonData)=>{
    this.Questions=jsonData.results
  })
  }

 

}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
