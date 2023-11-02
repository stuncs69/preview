<template>
  <div id="ui" class="d-flex flex-column justify-content-around">
    <VCard title="CTFLib opdrachten previewer ">
      <div class="d-flex flex-row justify-content-around">
        <input class="form-control w-50" type="file" ref="opdrachtFile" id="opdrachtFile" accept="application/JSON">
        <VButton @click="upload()" text="Laad opdracht"/>
        <!--<VButton @click.native="travel('delete')" text="Verwijder laatste opdracht uit cache"/>-->
      </div>
    </VCard>
    <VCard title="FAQ">
      <article>
        <h4>Waarom kan ik de CTF niet lokaal hosten?</h4>
        <hr>
        <p>Om de veiligheid van de applicatie te bewaren hebben we besloten om een aparte website te maken waarop er in
          een veilige omgeving gespeeld kan worden met JavaScript, zonder dat de CTF kans loopt op schade.</p>
      </article><br>
      <article>
        <h4>Hoe maak ik een opdracht voor de CTFv2?</h4>
        <hr>
        <p>Je kan vragen over de CTFv2 en de ontwikkeling van opdrachten ervoor in de <a href="https://discord.gg/2q6Byy4eKw">Discord server.</a></p>
      </article>
    </VCard>
  </div>
  <div id="opdracht">

  </div>
</template>

<style scoped>
#id {
  display: none;
  top: 0;
  left: 0;
  position: absolute;
}

#content {
  background-color: transparent;
  width: 100%;
  margin-top: -7rem;
  flex: 1;
  padding: 2rem;
  height: 70%;
}

#ui {
  top: 0;
  left: 0;
  position: absolute;
  background-image: url(https://ctf.cyberbrein.nl/img/ctf-red.webp);
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  z-index: 1;
  padding: 2rem;
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
  width: 96%;
  height: fit-content;
  background-color: white;
  padding: 1rem;
  margin: 2rem;
  margin: 2rem auto;
  border-radius: 2rem;
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
        document.querySelectorAll(`#${page.id}`).forEach(el => {
          el.style.display = "none";
        })
      })
      document.querySelector(`#${toPage}`).style.display = "block";
    },
    upload() {
		let file = this.$refs.opdrachtFile.files[0];
		let reader = new FileReader();
		reader.readAsText(file, "UTF-8");
		reader.onload = function (evt) {
			// alert(evt.target.result);
		}
		alert("Deze website is nog in aanbouw!")
    }
  },
}

</script>