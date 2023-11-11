<template>
  <div class="background" />
  <div id="ui" class="d-flex flex-row justify-content-around">
    <VCard title="CTFLib opdrachten previewer ">
      <div class="d-flex flex-row justify-content-around">
        <input class="form-control w-100" type="file" ref="opdrachtFile" id="opdrachtFile" accept="application/JSON">
        <!-- <VButton @click="upload()" text="Laad opdracht"/> -->
        <!--<VButton @click.native="travel('delete')" text="Verwijder laatste opdracht uit cache"/>-->
      </div>
	  	<br><br>
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
			</article><br>
			<article>
				<h4>Hoe werkt deze website?</h4>
				<hr>
				<p>Dit zijn de instructies van de CTFv2 preview website, waarin gemakkelijk opdrachten gemaakt met de CTFLib (<a href="https://www.npmjs.com/package/ctflib">NPM</a>) getest kunnen worden.</p>
				<h5>Het laden van een opdracht gaat als volgt:</h5>
				<ol>
					<li>Ga naar de CTFLib <a href="https://stuncs.space/preview/">preview website</a> (Als het goed is zit je daar nu op!)</li>
					<li>Upload de JSON bestand die gegenereerd is door CTFBuild (<a href="https://www.npmjs.com/package/ctfbuild">NPM</a>)</li>
				</ol>
				<p>Als het goed is bouwt de website zichzelf om naar de opdracht die jij gebouwt hebt. In deze omgeving is het mogelijk om te testen op bugs/fouten in de code.</p>
			</article>
    	</VCard>
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

.background {
	background-image: url(https://ctf.cyberbrein.nl/img/ctf-red.webp);
	z-index: -2;
	height: 100%;
	width: 100%;
	top: 0;
	left: 0;
	position: absolute;
}

#opdracht {
	height: 100%;
	width: 100%;
}

#ui {
  top: 0;
  left: 0;
  position: absolute;
  /* background-image: url(https://ctf.cyberbrein.nl/img/ctf-red.webp); */
  display: flex;
  flex-direction: column;
  width: 100%;
  height: max-content;
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
  mounted() {
	this.$refs.opdrachtFile.addEventListener('change', (e) => {
		this.upload()
	})
  },
  data() {
    return {
      page: "upload",
	  showModal: false
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
			console.log(evt.target.result);
			const parsed = JSON.parse(evt.target.result);

			// remove old UI
			document.getElementById("ui").remove()
			document.getElementsByClassName("background")[0].remove()

			// create new elements
			const script = document.createElement("script")
			const style = document.createElement("style")

			// render HTML & CSS first
			document.getElementById("opdracht").innerHTML = parsed.code.html;
			style.innerHTML = parsed.code.css;

			// render script
			script.innerHTML = parsed.code.js
			console.log(parsed)
		}
    }
  },
}

</script>