<template>
  <div class="wrapper">
    <h1> Знаю погоду не смотря в окно </h1>
    <p> Покажем погоду в {{ city == "" ? "вашем городе" : "`" + city + "`" }} </p>

    <input type="text" placeholder="Москва" v-model="city">

    <button v-if="city!=''" @click="getWeather()"> Узнать погоду </button>
    <button disabled v-else=""> Укажите город </button>

    <div v-if="info != null">
      <p> {{ cityName }} </p>
      <p> {{ cityTemp }} </p>
      <p> {{ cityFeelsLike }} </p>
      <p> {{ cityMinTemp }} </p>
      <p> {{ cityMaxTemp }} </p>
    </div>

    <p class="error"> {{ error }} </p>
  </div>
</template>

<style scoped>
  .wrapper{
    width: 900px;
    height: 500px;
    padding: 20px;
    text-align: center;
    border-radius: 50px;
    background-color: #1f0f24;
    color: white;
  }

  .wrapper h1{
    margin-top: 50px;
  }

  .wrapper p {
    margin-top: 20px;
  }

  .wrapper input{
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
  }

  .wrapper input:focus{
    border-bottom-color: #6e2d7d;
  }

  .wrapper button{
    padding: 10px 15px;
    margin-left: 20px;
    border: 2px solid #b99935;
    border-radius: 10px;
    background: #e3bc4b;
    color: #fff;
    cursor: pointer;
    transition: transform 500ms ease;
  }

  .wrapper button:hover{
    transform: scale(1.1) translateY(-3px);
  }

  .wrapper button:disabled{
    background: #746027;
    cursor: not-allowed;
    transition: none;
    transform: none;
  }

  .error{
    color: #d03939;
  }
</style>

<script>
import axios from "axios";
export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    };
  },

  computed: {
    cityName() {
      return "`" + this.city + "`";
    },
    cityTemp() {
      return "Температура: " + this.info.main.temp + "°C";
    },
    cityFeelsLike() {
      return "Ощущается как: " + this.info.main.feels_like + "°C";
    },
    cityMinTemp() {
      return "Минимальная температура: " + this.info.main.temp_min + "°C";
    },
    cityMaxTemp() {
      return "Максимальная температура: " + this.info.main.temp_max + "°C";
    },
  },

  watch: {
    city(newCity) {
      if (newCity.trim() === "") {
        this.info = null;
      }
    },
    
  },

  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Название города не может состоять из одной буквы!";
        return false;
      }
      this.error = "";

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=cdca4b86caa7b78c15d54a79c440233b`
        )
        .then((res) => (this.info = res.data))
        .catch(() => {
          this.error = "Не удалось получить данные. Проверьте название города.";
        });
    },
  },
};
</script>