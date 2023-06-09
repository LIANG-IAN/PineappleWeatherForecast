<script>
export default {
  data() {
    return {
      display: true,
      weatherInfo: null,
      click: null,
      city:null,
      weatherDescription:null,
      minTemperature:null,
      maxTemperature:null,
      chanceOfRain:null
    }
  }, methods: {
    showWeatherCard() {
      this.display = false;
      this.showWeather();
    },
    hideWeatherCard() {
      this.display = true;
    },
    showWeather() {
      const i = Math.floor(Math.random()*(this.weatherInfo.records.location.length));
      this.city = this.weatherInfo.records.location[i].locationName;
      this.weatherDescription = this.weatherInfo.records.location[i].weatherElement[3].time[1].parameter.parameterName;
      this.minTemperature = this.weatherInfo.records.location[i].weatherElement[2].time[1].parameter.parameterName;
      this.maxTemperature = this.weatherInfo.records.location[i].weatherElement[4].time[1].parameter.parameterName;
      this.chanceOfRain =  this.weatherInfo.records.location[i].weatherElement[1].time[1].parameter.parameterName;
    }
  },
  mounted() {
    fetch("https://opendata.cwb.gov.tw/api/v1/rest/datastore/F-C0032-001?Authorization=CWB-77C9064F-68B2-4267-AA2E-4EB580080BC8")
        .then(res => res.json())
        .then(data => {
          this.weatherInfo = data;
          console.log(data)
        })
  }
}

</script>

<template>
  <div class="h-screen bg-blue-300">
    <div class="flex justify-center">
      <div
          class="before:block before:absolute before:-inset-1 before:-skew-y-3 before:bg-pink-500 relative inline-block m-10">
        <h1 class="text-5xl relative text-white">
          神奇海螺
        </h1>
      </div>
    </div>
    <div class="flex justify-center">
      <img src="../img/logo.svg" alt="pinia" class="active:scale-110 duration-200" @mouseup="showWeather" @mouseenter="showWeatherCard" @mouseout="hideWeatherCard">
    </div>
    <div class="bg-blue-50 w-64 h-40 absolute bottom-96 left-96 rounded-3xl p-3" :class="{display:display}">
      <p class="text-2xl">{{city}}</p>
      <p class="text-2xl">{{weatherDescription}}</p>
      <span class="text-2xl">{{minTemperature}} ℃</span>
      <span class="text-2xl">~</span>
      <span class="text-2xl">{{maxTemperature}} ℃</span>
      <p class=text-2xl>{{chanceOfRain}} %</p>
    </div>
  </div>
</template>

<style>
.display {
  display: none;
}
</style>