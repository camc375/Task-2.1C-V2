<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div class="app">
    <header>
      <div class="header-content">
        <img alt="To Do logo" class="logo" src="@/assets/ToDo_logo.jpg" width="125" height="125" />

        <HelloWorld msg="Task 2.1C" />

        <nav>
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/list">List</RouterLink>
          <RouterLink to="/demo">Demo</RouterLink>
        </nav>
      </div>
    </header>

    <div class="content">
        <RouterView />
    </div>

  </div>


</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

header {
  text-align: center;
  padding: 2rem 0;
}

.header-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.content {
  flex: 1;
  padding: 1rem;
}

.logo {
  margin-bottom: 1rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
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

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
