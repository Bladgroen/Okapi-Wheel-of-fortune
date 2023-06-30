<template lang="">
  <div class="Drink">
    <div class="content">
      <img :src="getObjectFromAssortment(currentLetter).img" />
      <p>{{ getObjectFromAssortment(currentLetter).naam }}</p>
      <p>{{ getObjectFromAssortment(currentLetter).prijs }}</p>
      <p>{{ timerDisplay }}</p>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      assortment: {
        A: {
          img: "../../public/Corona.png",
          naam: "Anno 2020",
          prijs: "€3,10",
        },
        B: {
          img: "../../public/desperados.jpg",
          naam: "Bier op zijn mexicaans",
          prijs: "€3,10",
        },
        C: {
          img: "../../public/gerolsteinerCitroen.jpg",
          naam: "Citroentje",
          prijs: "€0,70",
        },
        D: {
          img: "../../public/strongbow.png",
          naam: "De boog moet niet altijd gespannen staan",
          prijs: "€3,10",
        },
        E: {
          img: "../../public/icetea.jpg",
          naam: "Eerst een theetje!",
          prijs: "€1,00",
        },
        H: {
          img: "../../public/wittewijn.jpg",
          naam: "Hoerendiezel",
          prijs: "€2,20",
        },
        I: {
          img: "../../public/colazero.jpg",
          naam: "Ik ben op dieet",
          prijs: "€0,90",
        },
        J: {
          img: "../../public/stellaZero.jpg",
          naam: "Jari's favourite",
          prijs: "€1,30",
        },
        K: {
          img: "../../public/Cola.jpg",
          naam: "Kunt niet altijd bier drinken",
          prijs: "€0,90",
        },
        L: {
          img: "../../public/Rosé.jpg",
          naam: "La Vie en rosé",
          prijs: "€2,20",
        },
        M: {
          img: "../../public/Duvel.jpg",
          naam: "Moet niet altijd een engeltje zijn",
          prijs: "€2,20",
        },
        O: {
          img: "../../public/Omer.jpg",
          naam: "Omer hoe beter",
          prijs: "€2,20",
        },
        R: {
          img: "../../public/Kriek.jpg",
          naam: "Roden bucht",
          prijs: "€1,90",
        },
        S: {
          img: "../../public/green.jpg",
          naam: "Spill the tea",
          prijs: "€1",
        },
        T: {
          img: "../../public/stella.jpg",
          naam: "T'is hier geen T-klub",
          prijs: "€1,50",
        },
        V: {
          img: "../../public/bruiswater.jpg",
          naam: "Voor de durvers onder ons",
          prijs: "€0,60",
        },
        W: {
          img: "../../public/water.jpg",
          naam: "Water voor de kater",
          prijs: "€0,60",
        },
        Z: {
          img: "../../public/Rouge.jpg",
          naam: "Zoals Marco Borsato zong: vandaag is rood de kleur van rouge",
          prijs: "€2",
        },
        "🌟": {
          img: "../../public/stella.jpg",
          naam: "🌟 LUCKY 🌟",
          prijs: "€1,20",
        },
        G: {
          img: "../../public/cornet.png",
          naam: "Goe, Cornetje?",
          prijs: "€2,30",
        },
      },
      countdown: 30 * 60,
      intervalId: null,
    };
  },
  props: {
    currentLetter: {
      type: String,
      required: true,
    },
  },
  computed: {
    timerDisplay() {
      const minutes = Math.floor(this.countdown / 60);
      const seconds = this.countdown % 60;
      return `${minutes}:${seconds < 10 ? "0" : ""}${seconds}`;
    },
  },
  methods: {
    getObjectFromAssortment(letter) {
      return this.assortment[letter] || {};
    },

    updateTimer() {
      if (this.countdown > 0) {
        this.countdown--;
      } else {
        clearInterval(this.intervalId);
        // Timer has reached 0, perform any required actions here
      }
    },
  },
  mounted() {
    this.intervalId = setInterval(this.updateTimer, 1000);
  },
  beforeUnmount() {
    clearInterval(this.intervalId);
  },
};
</script>
<style lang="scss">
.Drink {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 11;
  background-image: url("../DrinkPictures/background.png");
  background-repeat: no-repeat;
  background-size: cover;
  .content {
    padding-top: 1rem;
  }
  img {
    max-width: 300px;
    max-height: 500px;
    margin-top: 2rem;
  }

  p {
    font-size: 50px;
    font-weight: 600;
    color: white;
    @import url("https://fonts.googleapis.com/css2?family=Archivo+Black&display=swap");
    font-family: "Archivo Black", sans-serif;
  }
}
</style>
