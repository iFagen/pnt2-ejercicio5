<template >

  <section >
    <body>
      <div id="app">	    
        <div id="header" :style="{backgroundColor: mensajes.headerColor}">
        <h1>The Great <br>
          <span id="colorDisplay">{{pickedColor}}</span>
            <br>
            Guessing Game</h1>
        </div>

        <div id="navigator">
          <button id="reset" @click="reset()"> {{mensajes.restartButton}}</button>
          <span id="message"> {{mensajes.messageDisplay}} </span>


          <button id="easy" @click="easy()" :class="{'selected': !isHard}">easy</button>
          <button id="hard" @click="hard()" :class="{'selected': isHard}">hard</button>
        </div>

        <div id="container">
          <Cuadrado
            :mensajes="mensajes"
            :square="square"
            :set-all-colors-to="setAllColorsTo"
            :picked-color="pickedColor"
            v-for="(square,index) in squares"
            class="square"
            :key="index"
          >{{Cuadrado}}</Cuadrado>
<!--           <div v-for="(square,index) in squares" class="square" :key="index" > -->
         <!--    <Cuadrado  
              :picked-color="pickedColor"
              :square="square"
              :mensajes="mensajes"
              :set-all-colors-to="setAllColorsTo"
            /> -->  
        </div>     
      </div>
    </body>

  </section>

</template>

<script >

import Cuadrado from './Cuadrado.vue'

  export default  {
    name: 'juego',
    props: [],
    components: {
      Cuadrado
    },  
    mounted() {
        this.init()
    },
     data () {
      return {
          pickedColor : 'RBG', 
          mensajes : {
            headerColor : '',
            messageDisplay: '',
            restartButton : 'New colors'
          }, 
          colorCount: 6,
          isHard: true,
          colors: [],
          squares: []
        }
    }, 
    methods: {
      init(){
        for(let i=0; i<6; i++) {
          this.squares.push({
            display: 'block',
                  backgroundColor: ''
              })
          }
          this.restart();
      },
      reset() {
        this.restart()
      },   
      easy(){ 
        console.log("easyButton");        
          if (this.isHard) {       
              this.isHard = false;
              this.colorCount = 3                
              for (var i = 0; i < this.colorCount; i++) {
                  this.squares[(i+3)].display = "none";
              }
              this.restart();
          }
        },

        hard(){                           
            if (!this.isHard) {
                console.log("hardButton");
                this.isHard = true;
                this.colorCount = 6
                this.restart();
                for (var i = 3; i < 6; i++) {
                    this.squares[i].display = "block";
                }
            }
        },
        
      PickColor(){
            var quantity;
            if (this.isHard) {
                quantity = 6;
            } else {
                quantity = 3;
            }
            return Math.floor(Math.random() * quantity );
        },

      setAllColorsTo(color) {
        this.squares.forEach( square => {
          square.backgroundColor = color;
        })
      },		
        
      createNewColors(numbers){
        var arr = [];
        for (var i = 0; i < numbers; i++) {
          arr.push(this.createRandomStringColor());
        }
        return arr;
      },

      createRandomStringColor(){
        var newColor = "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() + ")" ;
        console.log(newColor);
        return newColor;
      },

      randomInt(){
          return Math.floor(Math.random() * 256);
      },

      restart(){
        this.colors = this.createNewColors(this.colorCount);
          console.log(this.colors)
        this.pickedColor = this.colors[this.PickColor()];
        this.mensajes.headerColor = "steelblue";
        this.mensajes.messageDisplay = "";
        this.mensajes.restartButton = "New Colors!";
        for (var i = 0; i <this.squares.length; i++) {
          this.squares[i].backgroundColor = this.colors[i];
          }
        }		
    }, 
    computed: {

    }
}


</script>

<style scoped lang="css">
body {
	background: #232323;
	margin: 0;
	font-family: "Montserrat", "Avenir";
}

h1 {
	font-weight: normal;
	line-height: 1.1;
	padding: 20px 0;

}
#navigator {

	background: #ffffff;
	height: 30px;
	text-align: center;
	margin: 0;
	margin-top: -30px;

}
#header {
	transition: all 0.3s;
	background: steelblue;
	text-transform: uppercase;
	text-align: center;
	margin: 0;
	color: white;
	
}
#colorDisplay {
	font-size: 200%;
}


.square {
	width: 30%;
	background: rgb(25, 0, 255);
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;

}
#container {
	margin: 20px auto;
	max-width: 600px;
}
#message {
	color: #ffffff;
	display: inline-block;
	width: 20%;
}

/* 
#messageBox {
	
} 
*/

.selected {
	background-color: rgb(46, 133, 204);
	color: white;
}
button {
	border: none;
	background-color: white;
	font-family: "Montserrat", "Avenir";
	text-transform: uppercase;
	height: 100%;
	font-weight: 700;
	letter-spacing: 1px;
	color: steelblue;
	transition: all 0.3s;
	outline: none;
}
button:hover {
	color: white;
	background-color: steelblue;
}
</style>
