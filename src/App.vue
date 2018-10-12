<template>
  <div id="app">
    <h1>Hint: {{ hint }} {{ word }} </h1>
    <button @click = "chooseWord">New game</button>
    <h2 id = "traces">{{ traces.join("") }}</h2>  
  <hr>
  <input  @keyup = "checkGuess" id = "guess" v-model = "charGuess" type = "text" maxlength="1">
  <h2> {{ message }} </h2>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      message: '',
      word: '',
      hint: '',
      wordSplited: [],
      traces: [],
      rightGuess: 0,
      charGuess: '',
      charUsed: [],
      wordsList: ["dog", "beer", "delorean"],
      hintsList: ["An animal", "A drink", "A car"]
    }
  },
  methods: {
      teste() {
        console.log("ok");
      },
      chooseWord() {
        var randomChoice = Math.floor((Math.random()*3));
        this.hint = this.hintsList[randomChoice];
        this.word = this.wordsList[randomChoice];
        this.makeTraces();
      },
      makeTraces() {
        this.rightGuess=0;
        this.traces = [];
        this.wordSplited = this.word.split("");
        for (var h=0; h < this.wordSplited.length;h++){
          this.traces.push("_ ");
          console.log("for");
        }
        
      },
      checkGuess() {
        
        
        // check if player already used the letter
        this.checkUsed();
       
        //check if there is a right answer
        for (var h = 0; h< this.wordSplited.length; h++){
            console.log("checando acertos");
         
         if(this.wordSplited[h] == this.charGuess){
            this.message = "Right guess"
            this.rightGuess++;
            this.traces[h]=this.charGuess;
          }
       
       }
        
         // check if the player won
         this.checkWinner();

         // reset the variable and wait for new player guess
         this.charGuess ="";
        
      },

      checkUsed() {
        // check if playter already used the letter

        for(var h = 0; h< this.charUsed.length; h++){
              
            if (this.charGuess == this.charUsed[h]){
              this.message = "You've already used this letter"
              this.charGuess="";
             return
            }
        }

        // add player guess to list of used letters
        this.charUsed.push(this.charGuess);
      },

      checkWinner(){
          
          if(this.rightGuess >= this.wordSplited.length){
            this.message = "We have a winner!!"
          }
          
      }
  }
}
</script>

<style>
  #guess {
    height: 200px;
    width: 200px;
    font-size:240px;
  }


</style>
