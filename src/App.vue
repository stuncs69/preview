<template>
  <canvas id="c"></canvas>
  <div id="ui">
    <div id="topBar">
        <VButton text="Upload nieuwe opdracht"/>
        <VButton text="Bekijk laatste opdracht"/>
        <VButton text="Verwijder laatste opdracht uit cache"/>
    </div>
    <div id="content">
      <VCard id="upload">
        <h1>Hello World</h1>
      </VCard>
      <VCard id="latest">
        <h1>geen sigma</h1>
      </VCard>
      <VCard id="delete">
        <h1>wel sigma</h1>
      </VCard>
    </div>
  </div>
</template>

<style scoped>

#content {
  background-color: transparent;
  width: 100%;
  flex: 1;
  padding: 2rem;
  height: 70%;
}

#ui {
  top: 0;
  left: 0;
  position: absolute;
  background-color: transparent;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  z-index: 1;
}

#c {
  top: 0;
  left: 0;
  position: absolute;
}

#topBar {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  width: 100%;
  height: 30%;
  top: 0;
  left: 0;
  position: absolute;
  background-color: transparent;
  padding: 1rem;
  z-index: 2;
}

</style>

<script>
import VButton from './components/VButton.vue';
import VCard from './components/VCard.vue';

export default {
  components: {
    VButton,
    VCard
  },
  data() {
    return {
      page: "upload"
    }
  },
  methods: {
    travel(toPage) {
      document.querySelectorAll("#content > div").forEach(page => {
        console.log(page)
      })
    }
  },
  mounted() {
    // geting canvas by Boujjou Achraf
    var c = document.getElementById("c");
    var ctx = c.getContext("2d");

    //making the canvas full screen
    c.height = window.innerHeight;
    c.width = window.innerWidth;

    //chinese characters - taken from the unicode charset
    var matrix = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@#$%^&*()*&^%+-/~{[|`]}";
    //converting the string into an array of single characters
    matrix = matrix.split("");

    var font_size = 10;
    var columns = c.width/font_size; //number of columns for the rain
    //an array of drops - one per column
    var drops = [];
    //x below is the x coordinate
    //1 = y co-ordinate of the drop(same for every drop initially)
    for(var x = 0; x < columns; x++)
        drops[x] = 1; 

    //drawing the characters
    function draw()
    {
        //Black BG for the canvas
        //translucent BG to show trail
        ctx.fillStyle = "rgba(0, 0, 0, 0.04)";
        ctx.fillRect(0, 0, c.width, c.height);

        ctx.fillStyle = "#f4427d";//green text
        ctx.font = font_size + "px arial";
        //looping over drops
        for(var i = 0; i < drops.length; i++)
        {
            //a random chinese character to print
            var text = matrix[Math.floor(Math.random()*matrix.length)];
            //x = i*font_size, y = value of drops[i]*font_size
            ctx.fillText(text, i*font_size, drops[i]*font_size);

            //sending the drop back to the top randomly after it has crossed the screen
            //adding a randomness to the reset to make the drops scattered on the Y axis
            if(drops[i]*font_size > c.height && Math.random() > 0.975)
                drops[i] = 0;

            //incrementing Y coordinate
            drops[i]++;
        }
    }

    setInterval(draw, 35);

  }
}

</script>