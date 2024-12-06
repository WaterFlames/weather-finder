<template>
  <div class="wrapper">
    <h1> Знаю погоду не смотря в окно </h1>
    <p> Покажем погоду в {{ city == "" ? "вашем городе" :city}} </p>

    <input type="text" placeholder="Москва" v-model="city">
    <button v-if="city!=''"> Узнать погоду </button>
    <button disabled v-else=""> Укажите город </button>
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
</style>

<script>
  export default {
    data(){
      return{
        city: ""
      }
    }
  };
</script>