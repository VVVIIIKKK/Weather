<template>
  <div class="main__content">
    <div class="main__content-left">
      <p class="main__content-left-degree">
        {{ Math.round(weather.current.temp) }}°
      </p>
      <p class="main__content-left-today">Сегодня</p>
      <p class="main__content-left-time">Время: {{ getTime }}</p>
      <p class="main__content-left-city">
        Город: {{ weather.name.toString() }}
      </p>
      <div class="main__content-left-img">
        <img :src="getImg" alt="" />
      </div>
    </div>
    <div class="main__content-right">
      <img src="@/assets/img/bg.svg" class="main__content-right-bg" alt="" />
      <div class="main__content-right-item">
        <div class="main__content-right-item-img">
          <img src="@/assets/img/temp.svg" alt="" />
        </div>
        <span>Температура</span>
        <p>{{ Math.round(weather.current.temp) }}° - ощущается как {{ Math.round(weather.current.feels_like) }}°</p>
      </div>
      <div class="main__content-right-item">
        <div class="main__content-right-item-img">
          <img src="@/assets/img/pressure.svg" alt="" />
        </div>
        <span>Давление</span>
        <p>{{weather.current.pressure}}мм ртутного столба </p>
      </div>
      <div class="main__content-right-item">
        <div class="main__content-right-item-img">
          <img src="@/assets/img/osadki.svg" alt="" />
        </div>
        <span>Осадки</span>
        <p>{{weather.current.clouds}}%</p>
      </div>
      <div class="main__content-right-item">
        <div class="main__content-right-item-img">
          <img src="@/assets/img/wind.svg" alt="" />
        </div>
        <span>Ветер</span>
        <p>{{weather.current.wind_speed}} м/c</p>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import { weatherName } from "@/icons";
export default {
  computed: {
    ...mapState(["weather"]),
    description(){
      return this.weather.current.weather[0].description
    },
    getImg(){
      return weatherName[this.description] || weatherName['ясно'];
    },
    getTime() {
      return new Date().toLocaleString("en-US", {
        timeZone: this.weather.timezone,
        timeStyle: "short", 
        hourCycle: 'h23',
      });
    },
  },
};
</script>

<style>
</style>