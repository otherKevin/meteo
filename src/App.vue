<template>
  <div id="mainDiv">
    <div class="headerDisplay">
      <Header :mainTitle="mainTitle" :tagline="tagline" />
    </div>

    <button class="btn" @click="getWeather">Consulter</button>
    <button class="btn" @click="getLocalWeather">Météo Locale</button>

    <div id="boxesZone">
      <Forecast
        v-for="element in prevList"
        :key="element.dt"
        :prevision="element"
      ></Forecast>
    </div>
    <div class="footerDisplay">
      <Footer :copyright="copyright" :links="links" />
    </div>
  </div>
</template>

<script>
import Forecast from "./components/Forecast.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
export default {
  components: {
    Forecast,
    Header,
    Footer,
  },

  data() {
    return {
      prevList: [],
      myLati: 5,
      myLongi: null,
      mainTitle: "MétéoBox",
      tagline: "Bienvenue sur le site de la météo",
      copyright: "© 2022 Meteobox.frud",
      links: "https://openweathermap.org",
    };
  },

  methods: {
    async getWeather() {
      let reponse = await fetch(
        "https://api.openweathermap.org/data/2.5/forecast?lat=43.7041622&lon=7.2743404&units=metric&appid=dbc8b6fc745f708c40c3e92db7d46a04"
      );
      let prevision = await reponse.json();

      this.prevList = prevision.list;
    },

    async getLocalWeather() {
      navigator.geolocation.getCurrentPosition((position) => {
        this.myLati = position.coords.latitude;
        this.myLongi = position.coords.longitude;

        console.log("variables de latitude et longitude temporaires :");
        console.log(this.myLati);
        console.log(this.myLongi);

        this.localWeatherFetch();
      });
    },

    async localWeatherFetch() {
      let response = await fetch(
        "https://api.openweathermap.org/data/2.5/forecast?lat=" +
          this.myLati +
          "&lon=" +
          this.myLongi +
          "&units=metric&appid=dbc8b6fc745f708c40c3e92db7d46a04"
      );
      let prevision = await response.json();
      this.prevList = prevision.list;
    },
  },
};
</script>

<style>
#mainDiv {
  inline-size: 90 em;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.btn {
  inline-size: 150px;
}
#boxesZone {
  padding-block-start: 20px;
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}
</style>
