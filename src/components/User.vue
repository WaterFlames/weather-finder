<template>
    <div class="user">
        <button @click="deleteUser(index)"> Delete </button>

        <h3>{{ user.name }}</h3>
        <p>{{ user.email }} - <b>{{ user.pass }}</b></p>
    </div>
</template>
  
<style scoped>
  .user{
    background-color: gray;
    color: white;
  }
</style>
  
<script>
    export default{
        props:{
            user:{
                type: Object,
                Required: true,
            },
            index:{
                type: Number,
                Required: true,
            },
            deleteUser:{
                type: Function,
                Required: true,
            },
        }
    }
</script>