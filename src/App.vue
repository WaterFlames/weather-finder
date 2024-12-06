<template>
  <div class="field">
    <!--main text-->
    <h1> I know the weather without looking out the window </h1>
    <p> We'll show you the weather {{ city == "" ? "in your city" : "`" + city + "`" }} </p>

    <!--input field-->
    <input type="text" placeholder="Moscow" v-model="city">

    <!--button settings-->
    <button v-if="city!=''" @click="getWeather()"> Check the weather </button>
    <button disabled v-else=""> Please enter a city </button>

    <!--output data-->
    <div v-if="info != null">
      <p> {{ cityName }} </p>
      <p> {{ cityTemp }} </p>
      <p> {{ cityFeelsLike }} </p>
      <p> {{ cityMinTemp }} </p>
      <p> {{ cityMaxTemp }} </p>
    </div>
    
    <!--error field-->
    <p class="error"> {{ error }} </p>
  </div>
</template>

<style scoped>
  .field{
    width: 900px;
    height: 500px;
    padding: 20px;
    text-align: center;
    border-radius: 50px;
    background-color: #1f0f24;
    color: white;
  }

  .field h1{
    margin-top: 50px;
  }

  .field p {
    margin-top: 20px;
  }

  .field input{
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
  }

  .field input:focus{
    border-bottom-color: #6e2d7d;
  }

  .field button{
    padding: 10px 15px;
    margin-left: 20px;
    border: 2px solid #b99935;
    border-radius: 10px;
    background: #e3bc4b;
    color: #fff;
    cursor: pointer;
    transition: transform 500ms ease;
  }

  .field button:hover{
    transform: scale(1.1) translateY(-3px);
  }

  .field button:disabled{
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
//enter variables
export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    };
  },

  // output data
  computed: {
    cityName() {
      return "`" + this.city + "`";
    },
    cityTemp() {
      return "Temperature: " + this.info.main.temp + "°C";
    },
    cityFeelsLike() {
      return "Feels like: " + this.info.main.feels_like + "°C";
    },
    cityMinTemp() {
      return "Min temperature: " + this.info.main.temp_min + "°C";
    },
    cityMaxTemp() {
      return "Max temperature: " + this.info.main.temp_max + "°C";
    },
  },

  //cleaning output data
  watch: {
    city(newCity) {
      if (newCity.trim() === "") {
        this.info = null;
      }
    },
    
  },

  //error handler + link
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "The name of the city cannot consist of one letter!";
        return false;
      }
      this.error = "";

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=cdca4b86caa7b78c15d54a79c440233b`
        )
        .then((res) => (this.info = res.data))
        .catch(() => {
          this.error = "Failed to retrieve data. Check the city name.";
        });
    },
  },
};
</script>