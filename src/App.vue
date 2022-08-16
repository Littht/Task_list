<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/list">List</router-link>
  </nav>
  <router-view/>
</template>

<style>
*{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  box-sizing: border-box;
  padding: 0;
  margin:0;
  font-size: 16px;
}
body{
  width: 100%;
  height: 100vh;
  background-color: #f2f2f2;
}
nav{
  background-color: rgb(0, 224, 86); 
  position: relative;
  width: 100%;
  height: 60px;
  display: flex;
  align-items: center;
  gap: 1em;
}

nav a{
  text-decoration: none;
  padding: 10px 20px;
  background: white;
  border-radius: 4px;
}
nav a:nth-child(1){
  margin-left: 20px;
}

</style>
