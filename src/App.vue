<template>
  <div id="app">
    <header>
      <router-link to="/">
        <h1><span>Jarvi's </span>Movie App</h1>
      </router-link>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
  background: transparent(#42b883, 0.5);
}

body {
  background-color: #355e5e;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  margin-bottom: 10px;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 7px rgba(0, 0, 0, 0.3);
}

h1 {
  color: #fff;
  font-size: 28px;
}
span {
  color: #42b883;
}
</style>
