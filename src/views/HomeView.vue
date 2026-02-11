<script setup>
import { ref } from 'vue';
import CreatePoll from "../components/CreatePoll.vue";
// import TheWelcome from "../components/TheWelcome.vue";
import PollCreated from "@/components/PollCreated.vue";

const linkToPoll = ref('');
const updateLinkToPoll = (value) => {
  console.log('received: ' + value);
  var receivedPoll = JSON.parse(value);
  linkToPoll.value = window.location.href + "?pid=" + receivedPoll.id;
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

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
