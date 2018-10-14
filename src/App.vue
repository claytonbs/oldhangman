<template>
  <div id="app">
    
    <nav>
      <button @click = "chooseWord">New game</button>
    </nav>
    <h1 v-if="!isRunning">Welcome to the hangman game! </h1>
    
    <h1 v-if="isRunning">Hint: {{ hint }} {{ word }} </h1>


        
  <svg id = "drawning" width="640" height="400" xmlns="http://www.w3.org/2000/svg" xmlns:svg="http://www.w3.org/2000/svg">
 <!-- Created with SVG-edit - http://svg-edit.googlecode.com/ -->
 <g  id = "hang">
  <title>Layer 1</title>
  <ellipse id="svg_2" cy="69.4" cx="23" stroke-width="5" stroke="#000000" fill="#FF0000"/>
  <rect id="svg_3" height="299" width="45" y="88.4" x="95" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="0" stroke="#000000" fill="#7f0000"/>
  <rect stroke="#000000" transform="rotate(-90 185.875,110.39999389648436) " id="svg_5" height="143.000002" width="43.875001" y="38.899993" x="163.9375" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="0" fill="#7f0000"/>
  <line stroke-width="2" id="svg_6" y2="175.4" x2="228" y1="131.4" x1="227" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke="#7f3f00" fill="none"/>
  <rect stroke="#000000" stroke-width="0" transform="rotate(-40.67490768432617 152.8824462890625,144.5350799560547) " id="svg_8" height="11.25" width="63.204397" y="138.910076" x="121.280243" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" fill="#7f3f00"/>
  <circle id="svg_10" r="2.767424" cy="161.102339" cx="133.328481" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="0" stroke="#000000" fill="#7f7f7f"/>
  <circle id="svg_11" r="2.767424" cy="126.825022" cx="172.404706" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="0" stroke="#000000" fill="#7f7f7f"/>
 </g>
 <g id = "head" v-if="wrongGuess>=1">
  <title>Camada 2</title>
  <circle stroke="#ff0000" id="svg_12" r="25.650152" cy="201.300017" cx="228.16245" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" fill="#000000"/>
 </g>
 <g id = "body" v-if="wrongGuess>=2">
  <title>corpo</title>
  <line stroke="#ff0000" id="svg_13" y2="281.350251" x2="228.724953" y1="226.761931" x1="228.724953" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" fill="none"/>
 </g>
 <g id = "rightarm" v-if="wrongGuess>=3">
  <title>bracoesq</title>
  <line id="svg_15" y2="282.976776" x2="198.499365" y1="234.039275" x1="228.874366" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" stroke="#ff0000" fill="none"/>
 </g>
 <g id = "leftarm" v-if="wrongGuess>=4">
  <title>bracodir</title>
  <line stroke="#ff0000" id="svg_16" y2="283.186394" x2="253.855592" y1="234.782829" x1="228.879273" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" fill="none"/>
 </g>
 <g id = "rightleg" v-if="wrongGuess>=5">
  <title>pernaesq</title>
  <line stroke="#ff0000" id="svg_17" y2="327.177532" x2="199.046819" y1="280.94267" x1="228.808783" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" fill="none"/>
 </g>
 <g id = "leftleg" v-if="wrongGuess>=6">
  <title>pernadir</title>
  <line stroke="#ff0000" transform="rotate(180 240.59318542480466,304.0843505859375) " id="svg_18" y2="327.201794" x2="252.542446" y1="280.966932" x1="228.643915" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" fill="none"/>
  <line id="svg_19" y2="195.46999" x2="222.570616" y1="185.740498" x1="215.68878" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" stroke="#ff0000" fill="none"/>
  <line id="svg_20" y2="196.033588" x2="215.388441" y1="185.354878" x1="222.507581" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" stroke="#ff0000" fill="none"/>
  <line id="svg_22" y2="195.251995" x2="240.25984" y1="185.522503" x1="233.378004" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" stroke="#ff0000" fill="none"/>
  <line id="svg_23" y2="195.815594" x2="233.077665" y1="185.136883" x1="240.196806" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" stroke="#ff0000" fill="none"/>
  <line stroke="#ff0000" id="svg_24" y2="209.77795" x2="245.386698" y1="209.77795" x1="213.642783" fill-opacity="0" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" fill="none"/>
  <path stroke="#ff0000" d="m223.053391,210.20089c-0.100113,0.899322 -0.132767,1.834711 -0.098022,2.756751c0.035904,0.952881 0.25325,1.836193 0.398819,2.784391c0.138,0.898844 -0.027344,1.875239 0.26091,2.729446c0.297928,0.882882 0.835815,1.622403 1.564987,2.107924c0.723755,0.481921 1.536057,0.807386 2.395477,0.90982c0.874084,0.104187 1.79274,0.03073 2.605606,-0.210541c0.902435,-0.267859 1.741241,-0.571531 2.449692,-1.113399c0.705505,-0.539606 1.084473,-1.451896 1.134613,-2.376261c0.048965,-0.902875 -0.073547,-1.829136 -0.400452,-2.675616c-0.323898,-0.838674 -0.400452,-1.7646 -0.400452,-2.663126l0,-0.940694l0,-0.941347l0.100113,-0.900405" id="svg_28" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" fill="#cc0808"/>
  <line id="svg_29" y2="213.482128" x2="227.858818" y1="209.77795" x1="227.858818" stroke-linecap="null" stroke-linejoin="null" stroke-dasharray="null" stroke-width="null" stroke="#ff0000" fill="none"/>
 </g>
</svg>


    <h2 id = "traces">{{ traces.join("") }}</h2>  
  <h3 v-if="isRunning"> {{ message }} </h3>
  <input v-bind:disabled="wrongGuess >= 6" v-if="isRunning"  @keyup = "checkGuess" id = "guess" v-model = "charGuess" type = "text" maxlength="1">
  <p v-if="charUsed.length > 0">Letters alread used: <span> {{ charUsed.join() }} </span></p>
  
  
  

  
  
  
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      message: 'Type a letter here:',
      word: '',
      hint: '',
      wordSplited: [],
      traces: [],
      rightGuess: 0,
      wrongGuess: 0,
      charGuess: '',
      charUsed: [],
      isRunning: false,
      wordsList: ["dog", "beer", "delorean"],
      hintsList: ["An animal", "A drink", "A car"]
    }
  },
  methods: {
      teste() {
        console.log("ok");
      },
      chooseWord() {
        this.rightGuess = 0;
        this.wrongGuess = 0;
        this.charUsed = [];
        this.isRunning = true;
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
        
        // reset the message
        this.message = "";
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
        

          // if there is no right guess check if the player lost (and update mistake count)
          if (this.message == "") {
              this.message = "Not a good try! :("
              this.wrongGuess++;
              this.checkLoser();

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
      checkLoser() {
        if (this.wrongGuess >= 6){
          this.message = "You LOST"

        }
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
@import url('https://fonts.googleapis.com/css?family=Raleway:300');


h1, h2, h3, p {
  margin-left: 10px;
}

p {
  margin-top: 30px;
}

#traces {
  margin-left: 80px;
}


body {
  font-family: 'Raleway', sans-serif;
  
  background-color:#1A1A1D;
  color: white;
  margin: 0;
}

nav {
  background-color: purple;
  margin-top: 10px;
}

nav button {
  outline: none;
  margin-left: 20px;
  background-color: purple;
  color: white;
  
  border: none;
  height: 25px;

}


nav button:hover {
  background-color: black;
  cursor: pointer;

}

  #guess {
    margin-left: 10px;
    height: 130px;
    width: 130px;
    font-size:140px;
    background-color: #1A1A1D;
    color: white;
    
  }


  #drawning {
    position: relative;
    top: -90px;
    right: 85px;
    z-index: -1;
    margin-bottom: -151px;
    /* background-color: red; */
  }

</style>
