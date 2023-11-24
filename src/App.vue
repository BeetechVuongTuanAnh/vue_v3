<script setup lang="ts">
import { RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Nav from './components/Nav.vue';
import { ref, reactive, computed, watch, watchEffect } from 'vue';

const title = ref('Hello');

const searchText = ref('');

let peoples = reactive(["Tuấn Anh", "Hưng", "Yến", "Thanh"])

const onChangeSomething = () => {
  console.log("on change something");
  title.value = title.value == 'Hello' ? 'Hi' : 'Hello';
}

const peopleFilled = computed(() => {
  peoples.map(people => {
    people = people.toLowerCase();
    return people;
  }).filter(people => people.includes(searchText.value.toLowerCase()))
})

watch(searchText, (newVal, oldVal) => {
  console.log(newVal, oldVal);
})

watchEffect(() => {
  if (searchText.value) {
    console.log("run again");

  }
})
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    <h1>{{ title }}</h1>
    <input type="text" v-model="searchText">
    <h2>Người dùng:</h2>
    <ul>
      <li v-for="(people, index) in peopleFilled" :key="index">
        {{ people }}
      </li>
    </ul>
    <!-- <button @click="onChangeSomething">Click me</button> -->
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <Nav></Nav>
    </div>
  </header>

  <RouterView />
</template>

<style>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
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
