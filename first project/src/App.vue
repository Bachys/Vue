<script>
import axios from 'axios'

export default {
  data () {
    return {
      city: "",
      error: "",
      info: null
    }
  },
  methods: {
    getWeather() {
      if(this.city.trim().length < 2) {
        this.error = 'Название должно быть более одного символа';
        return false
      }
      this.error = ''

      axios.get(``)  // Ссылка на APi
        .then(res => (this.info = res.data))
    }
  },
  computed: {
    showTemp () {
      return "Текущая температура: " + this.info.main.temp
    },
    showHumidity () {
      return "Влажность: " + this.info.main.humidity
    },
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в <span class="city-color">{{ city }}</span> </p>
    <input type="text" v-model="city" placeholder="Введите город">
    <button v-if="city != ''" @click="getWeather()">Получить погоду</button>
    <button v-else disabled>Введите город</button>
    <p class="error">{{ error }}</p>
    <div v-if="info != null">
      <!-- <p>{{ info.main }}</p>-->
      <p>{{ showTemp }}</p>
      <p>{{ showHumidity }}</p>
    </div>
    
  </div>
</template>

<style scoped>
  
  .wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    background: rgb(39, 36, 53);
    padding: 20px;
    text-align: center;
    color: #cfc8c8;
    font-family:Verdana, Geneva, Tahoma, sans-serif;
    margin-top: 100px;
  }

  .wrapper h1 {
    margin-top: 50px;
  }

  .wrapper p {
    margin-top: 20px;
  }

  .wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 1px solid #7bd226;
    color: rgb(255, 255, 255);
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
  }
  .wrapper input:focus {
    border-bottom-color: #00d4ff;
  }

  .wrapper button {
    padding: 5px 8px;
    color: rgb(0, 0, 0);
    background: rgb(2,0,36);
    background: linear-gradient(83deg, rgba(2,0,36,1) 0%, rgba(123,210,38,1) 0%, rgba(0,212,255,1) 100%);
    border-radius: 5px;
    border: none;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 1s ease;
  }

  .wrapper button:hover {
    transform: scale(1.1);
  }

  .wrapper button:disabled {
    background: rgb(2,0,36);
    background: linear-gradient(266deg, rgba(2,0,36,1) 0%, rgba(123,210,38,1) 0%, rgba(0,212,255,1) 100%);
    cursor: no-drop;
  }

  .city-color {
    font-size: 18px;
    color: #00d4ff;
  }

  .error {
    color: red;
    font-weight: bold ;
  }
</style>
