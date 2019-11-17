<template>
  <div id="app">
    <header></header>
    <main class="container-fluid">
      <router-view />
    </main>
    <footer></footer>
  </div>
</template>

<style>
body {
  font-family: Arial, Helvetica, sans-serif;
  background: #e7e5e5;
  color: rgb(51, 51, 51);
}
.container-fluid {
  margin-top: 2%;
  margin-bottom: 2%;
}
</style>
