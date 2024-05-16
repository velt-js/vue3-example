<script setup>
import { onMounted } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

import { initVelt } from '@veltdev/client'

let veltClient;

const initializeVelt = async () => {
  // Initialize the Velt client with your API key
  veltClient = await initVelt("hny91vx3KUxEIp61jBd1");
  setDocumentId();
  identifyUser();
}

/**
 * To set the document ID for the Velt client
 */
const setDocumentId = () => {
  if (veltClient) {
    veltClient.setDocumentId("pendo-velt-integration-customization");
  }
}

/**
 * To identify the user for the Velt client
 */
const identifyUser = () => {
  if (veltClient) {
    // Replace the user object with your user data
    const user = {
      userId: "1",
      email: "test@velt.dev",
      name: "Test User"
    };
    veltClient.identify(user);
  }
}

onMounted(() => {
  // Call the initializeVelt function when the component is mounted
  initializeVelt();
});
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    
    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <div class="actions-container">
        <!-- Velt comment tool to add pin comments -->
        <velt-comment-tool></velt-comment-tool>
      </div>
    </div>
  </header>
  
  <main>
    <velt-comments priority="true"></velt-comments>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.actions-container {
    margin: 16px 0;
    min-height: 40px;
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
}
</style>
