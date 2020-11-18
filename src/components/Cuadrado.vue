<template >
  <section class="cuadrado">
      <div
        :style="square" 
        @click="sqClick()"
      ></div>
  </section>

</template>

<script>

  export default  {
    name: 'Cuadrado',
    props: [
           'square'
          ,'pickedColor'
          ,'mensajes'
          ,'setAllColorsTo'
        ],
    data () {
      return {

      }
    },
    methods: {
        sqClick(){
          console.log("Cuadrado")
          var clickedColor = this.square.backgroundColor;
          console.log(clickedColor,this.pickedColor)

          if (clickedColor === this.pickedColor) {
            this.mensajes.messageDisplay = "You Picked Right!";
            this.setAllColorsTo(this.pickedColor);
            this.mensajes.restartButton = "Play Again!";
            //console.log('this.pickedColor',this.pickedColor)
            this.mensajes.headerColor = this.pickedColor;
          } else {
            this.square.backgroundColor = "#232323";
            this.mensajes.messageDisplay = "Try Again!";
          }
        }
    },
    computed: {
        getEstilos() {
          //console.log(this.square)
          return this.square
        }
    }
}


</script>

<style scoped lang="css">

</style>
