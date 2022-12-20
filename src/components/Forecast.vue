<template>
  <div class="boiteMeteo">
    <p>Ville : {{ cityName }}</p>
    <p>Température minimale :{{ prevision.main.temp_min }} °C</p>
    <p>Température maximale :{{ prevision.main.temp_max }}°C</p>
    <p>Vitesse du vent :{{ prevision.wind.speed }} km/h</p>
    <p>{{ prevision.weather[0].description }}</p>
    <img
      :src="
        `http://openweathermap.org/img/wn/` +
        prevision.weather[0].icon +
        `@2x.png`
      "
      alt="icon"
    />
    <p class="coldAlert" v-if="prevision.main.temp_min < 0">Alerte Froid</p>
    <p class="heatAlert" v-if="prevision.main.temp_max > 30">Alerte Chaud</p>
    <p class="windAlert" v-if="prevision.wind.speed > 40">Alerte Termpête</p>
  </div>
</template>

<script>
const Forecast = {
  props: {
    prevision: Array,
    /* cityName: String,
    minTemp: Number,
    maxTemp: Number,
    windSpeed: Number,
    description: String,
    meteoIcon: String,
    */
  },
};
export default Forecast;
</script>

<style scoped>
.boiteMeteo {
  display: flex;
  flex-direction: column;
  text-align: center;
  inline-size: 200px;
  block-size: 500px;
  border: 2px solid black;
  margin: 5px;
  background-color: aqua;
}
.coldAlert {
  color: aqua;
  background-color: lightslategray;
}
.heatAlert {
  color: red;
  background-color: yellow;
}
.windAlert {
  color: black;
  background-color: violet;
}
</style>
