<script> 
import axios from 'axios'

export default {
  data() {
    return {
      city: '',
      error: '',
      country: null,
      temp_c: null,
      region: null,
      precip_mm: null,
      last_updated: null
    }
  },
  computed: {
    cityName() {
      return "<" + this.city + ">";
    }
  },
  methods: {
    getWeather() {
      if(this.city.trim().length < 2) {
        this.error = 'Нужно звание более одного символа'
        return false;
      }
      this.error = '';

      axios.get(`http://api.weatherapi.com/v1/current.json?key=0a22dfa6f5f0407c8e8213332242804&q=${this.city}&aqi=no`)
      .then(res => {
          this.country = res.data.location.country;
          return res.data;
      })
      .then(data => {
          this.region = data.location.region;
          return data;
      })
      .then(data => {
          this.temp_c = data.current.temp_c;
          return data;
      })
      .then(data => {
          this.precip_mm = data.current.precip_mm;
          return data;
      })
      .then(data => {
          this.last_updated = data.current.last_updated;
      });
    }
  }
}
</script>

<template>
  <div className='wrapper'>
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в городе: {{ city == "" ? "Вашем городе" : cityName }}</p>
    <input v-model="city" type="text" placeholder="Введите город">
    <button v-show="city != ''" @click="getWeather()">Узнать погоду</button>
    <p className='error'>{{ error }}</p>
    <div v-show="country != null && temp_c != null && region != null">
      <p>Страна: {{ country }}</p>
      <p>Регион: {{ region }}</p>
      <p>Температура в цельсиях: {{ temp_c }}</p>
      <p>Осадки в миллиметрах: {{ precip_mm }}</p>
      <p>Последнее обноновление: {{ last_updated }}</p>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: red;
}

.wrapper {
  width: 900px;
  height: 500px;
  background-color: #121212;
  border-radius: 100px;
  padding: 20px;
  text-align: center;
  color: white;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0px;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
  border-bottom: 2px solid #110813;
}

.wrapper input:focus{
  border-bottom-color: #5219d6;
}

.wrapper button{
  background: #0ff7d8;
  color: white;
  border-radius: 10px;
  border: 2px solid #007767;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover{
  transform: scale(1.1) translateY(-3px)
}
</style>