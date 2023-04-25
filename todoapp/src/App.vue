<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>
<template>
  <div class="container">

    <header>
      <img alt="Vue logo" class="logo" src="@/assets/boy.png" width="350" height="890" />
      <div class="wrapper">
        <HelloWorld />
        <nav>
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
          <RouterLink to="/todo">Todo</RouterLink>
        </nav>
      </div>
    </header>
    <div class="slls">
      <RouterView />
    </div>
  </div>
</template>
<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  padding: 0 1rem;
}
.logo {
  display: block;
  margin: 0 auto 2rem;
  max-width: 100%;
}
.wrapper {
  flex-basis: 50%;
}
nav {
  width: 120%;
  font-size: 20px;
  text-align: center;
  margin-top: 2rem;
  margin-left: -1.5rem;
}
nav a.router-link-exact-active {
  color: var(--color-text);
}
nav a.router-link-exact-active:hover {
  background-color: transparent;
}
nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}
nav a:first-of-type {
  border: 0;
}
@media (min-width: 768px) {
  header {
    flex-wrap: nowrap;
    padding: 0;
  }
  .logo {
    margin: 0 2rem 0 0;
    max-width: none;
  }
  .wrapper {
    flex-basis: auto;
    margin: 0 2rem;
  }
}
</style>