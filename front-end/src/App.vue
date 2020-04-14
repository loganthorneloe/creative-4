<template>
<div id="app">
  <div class="menu">
    <ul>
      <li><a><img src="/images/pokemon_images/pikachu.png"></a></li>
      <li><a><router-link to="/">Pokemon</router-link></a></li>
      <li><a><router-link to="/admin">Team Builder</router-link></a></li>
    </ul>
  </div>

  <div class="title">
    <h1>Gen 1 Pokemon Team Builder</h1>
  </div>

  <div class="content">
    <router-view />
  </div>

  <div class="footer">
    <a href="https://github.com/lathorne/creative-4">https://github.com/lathorne/creative-4</a>
    <div> Logan Thorneloe & Clint Frandsen</div>
  </div>
</div>
</template>

<style>
html {
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
  font-size: 16px;
  background: #fff;
  padding: 0px;
  margin: 0px;
}

/* Header */
.menu {
  text-align: center;
}

.title {
  margin-top: 5px;
}

.title h1 {
  font-size: 30px;
}

.content {
  padding: 20px 100px;
  min-height: 500px;
}

/* Footer */
.footer {
  height: 50px;
  padding: 20px 100px 0px 100px;
  background: #e3e3e3;
  font-size: 12px;
}

.footer a {
  color: #000;
}

h1 {
  font-size: 20px;
}

h2 {
  font-size: 14px;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

li {
  float:left;
  background: none !important;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 25px 16px !important;
  text-decoration: none;
}

li a:hover:not(.active-menu){
  background-color: #111 !important;
}

.active-menu {
  background-color: #4CAF50 !important;
}

li a img{
  height: 60px ;
  vertical-align: center;
}

</style>
