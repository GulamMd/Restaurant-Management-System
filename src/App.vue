<template>
  <router-view />
</template>

<script>

export default {
  name: 'App',
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 
}
body{
  padding: 0;
  margin: 0;
}
.logo {
    width: 160px;
}
.register input,.login input,.add input,.update input{
    width: 300px;
    height: 50px;
    padding-left: 15px;
    display: block;
    margin-bottom: 20px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}
.register button,.login button ,.add button ,.update button{
    width: 312px;
    height: 45px;
    border: 1px solid skyblue;
    color: #fff;
    background-color: skyblue;
    cursor: pointer;
}
</style>
