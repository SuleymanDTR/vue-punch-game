<template>
  <div id="app">
    <!-- bag image -->
    <div id="bag" v-bind:class="{ burst: ended }" v-on:click="vur"></div>
    <!-- bag health bar -->
    <div id="bag-health">
        <div v-bind:style="{ width: health + '%' }"></div>
    </div>
    <!-- game control buttons -->
    <div id="controls">
        <a v-on:click="vur">Vur</a>
        <a v-on:click="tekrarla">Tekrarla</a>
    </div>
    <!-- music -->
    <a v-on:click="muzik" class="muzik">Müzik</a>
    <audio ref="musicElm" hidden autoplay>
      <source src="src/assets/music.mp3" type="audio/wav">
    </audio>
    <audio ref="audioElm" hidden>
      <source src="src/assets/punch.wav" type="audio/wav">
    </audio>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
        health : 100,
        ended : false,
        music : true
    }
  },
  methods : {
      vur : function(event) {
        if (!this.ended) {
          this.$refs.audioElm.pause();
          this.health -= 10;
          this.$refs.audioElm.play();
        }
        if(this.health <= 0) {        
          this.ended = true;
        }      
      },
      tekrarla : function() {
        this.health = 100;
        this.ended = false;
      },
      muzik : function(event) {
        this.music = !this.music;
        if(this.music)
          this.$refs.musicElm.play();
        else
          this.$refs.musicElm.pause();
      }
  }  
}
</script>

<style scoped>

#bag {
  background-image : url('./assets/bag.png');
  background-position: center center;
  background-repeat: no-repeat;
  background-size:70%;
  margin : 0 auto;
  height:400px;
  width:200px;
}

#bag.burst {
  background-image : url('./assets/bag-burst.png')
}

#controls {
  margin : 0 auto;
  width: 220px;
  text-align:center;
}
#controls a {
  display:inline-block;
  width:100px;
  padding : 5px 10px;
  text-align :center;
  background-color : red;
  color : #fff;
  border-radius :5px;
  box-sizing:border-box;
  cursor : pointer;
}

#bag-health {
  width:220px;
  border : 2px solid #000;
  height:20px;
  margin : 0 auto;
  margin-bottom:20px;
}
#bag-health > div {
  height:20px;
  background: #000;
  width:20px;
}

.muzik {
  position:absolute;
  border : 2px solid #333;
  background-color : #ccc;
  border-radius: 50%;
  text-align:center;
  width:50px;
  height:50px;
  line-height: 50px;
  top:10%;
  left:10%;
  cursor: pointer;
}

</style>
