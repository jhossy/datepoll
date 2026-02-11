<script setup>
import { ref } from 'vue';
import CreatePoll from "../components/CreatePoll.vue";
// import TheWelcome from "../components/TheWelcome.vue";
import PollCreated from "@/components/PollCreated.vue";

const linkToPoll = ref('');
const updateLinkToPoll = (value) => {
  console.log('received: ' + value);
  var receivedPoll = JSON.parse(value);
  linkToPoll.value = 'http://google.com?pid=' + receivedPoll.id;
}
</script>

<template>
  <header>
    <CreatePoll @poll-created="updateLinkToPoll"/>   
  </header>
  <div class="wrapper">
      <!-- <TheWelcome />       -->
       <PollCreated :link-to-poll="linkToPoll"/>
  </div>
</template>

<style scoped>
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
