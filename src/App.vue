<template>
    <nav>
      <router-link :to="{ name: 'home' }"><h1>Vue Movie</h1></router-link>
  </nav>
  <router-view/>
</template>

<style>
body{
  background-color: rgb(63, 98, 150);
}
.dark{
  background-color: #1d1d1d; 
  color: #fff;
}
nav{
  margin: 20px 30px;
  background-color: #39644c;
  color: #fff;
  padding: 1rem;
  text-align: center;
  border-radius: 20px;
}
a{
  text-decoration: none;
  color: #fff;
}
h1{
  font-size: 30px;
  font-weight: 700;
  color: white
}

</style>
