<template>
  <div id="ui">
    <div id="topBar">
        <VButton @click.native="travel('upload')" text="Upload nieuwe opdracht"/>
        <VButton @click.native="travel('latest')" text="Bekijk laatste opdracht"/>
        <VButton @click.native="travel('delete')" text="Verwijder laatste opdracht uit cache"/>
    </div>
    <div id="content">
      <VCard id="upload" style="display: block;">
        <h1>Test1</h1>
      </VCard>
      <VCard id="latest" style="display: none;">
        <h1>Test2</h1>
      </VCard>
      <VCard id="delete" style="display: none;">
        <h1>Test3</h1>
      </VCard>
    </div>
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
    }
  },
}

</script>