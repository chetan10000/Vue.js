<template>
<div class="question-box">
 <b-jumbotron>
  

    <template v-slot:lead>
 Questions.
 {{ currentQuestion.question }}
    </template>

    <hr class="my-4">

    <b-list-group>
  <b-list-group-item v-for="(answer,index) in answers" :key="index" @click="selectAnswer(index)" :class="[selectedIndex === index ? 'selected' : '']">

{{ answer }}
  </b-list-group-item>

</b-list-group>
      
     
   

    <b-button  variant="primary" @click="correctAnswer()" class="m-2" :disabled="selectedIndex===null || answered">Submit</b-button>
    <b-button @click="next" variant="success" href="#" m-2>Next</b-button>
  </b-jumbotron>
</div>
  </template>
  <script>
  import _ from 'lodash'

  export default {
    props: {
      currentQuestion:Object,
      next:Function,
      increament:Function
     
    },
    data: function(){
      return {
        answered:false,
        correctIndex:null,
        selectedIndex:null ,
        shuffleAnswers: []
      }
    },
    computed:{
      answers(){
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
        console.log(this.currentQuestion.correct_answer)
        return answers
      }
    },
    watch:{
      currentQuestion:{
        immediate:true,
        handler(){
        this.answered =false
        this.selectedIndex = null
        this.suffleIndex()
        }
      }
    },
    methods: {
                selectAnswer(index){
                                        this.selectedIndex = index
                                            console.log(this.currentQuestion)
        
                        },
                                              correctAnswer(){
                                                let isCorrect =false
                                                         if(this.selectedIndex === this.correctIndex){
                                               isCorrect=true
                                               this.increament(isCorrect)
                                               
                                                    }
                                              this.answered = true
                                             
                               
                                        }
      ,
      suffleIndex(){
        let answers = [...this.currentQuestion.incorrect_answers , this.currentQuestion.correct_answer]
        this.shuffleAnswers = _.shuffle(answers)
       this.correctIndex = this.shuffleAnswers.indexOf(this.currentQuestion.correct_answer)
  
        

      }
    }
  }
  </script>
  <style scoped>
  .selected{
background-color:lightblue;
  }
  .correct{
background-color: lightgreen;
  }
  .wrong{
background-color: brown;
  }

  </style>