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

  <!-- Velt feature customization -->
  <velt-wireframe>
    <!-- Updated the order of components -->
    <velt-comment-dialog-wireframe>
      <div class="comment-dialog-container">
          <velt-comment-dialog-composer-wireframe></velt-comment-dialog-composer-wireframe>
          <velt-comment-dialog-header-wireframe></velt-comment-dialog-header-wireframe>
          <velt-comment-dialog-body-wireframe></velt-comment-dialog-body-wireframe>
      </div>
    </velt-comment-dialog-wireframe>

    <!-- Replaced Comment Tool with custom tool -->
    <velt-comment-tool-wireframe>
      <div class="comment-tool">
        <svg xmlns="http://www.w3.org/2000/svg" width="40px" height="40px" viewBox="0 0 1024 1024" class="icon" version="1.1">
          <path d="M298.155 403.601c-43.565 0.395-56.901 16.984-56.901 37.934 0 20.952 15.113 37.935 56.901 37.935 41.79 0 56.905-16.984 56.905-37.935s-13.338-38.331-56.905-37.934z m227.614 0c-43.567 0.395-56.905 16.984-56.905 37.934 0 20.952 15.115 37.935 56.905 37.935 41.788 0 56.901-16.984 56.901-37.935 0.001-20.951-13.336-38.331-56.901-37.934z m142.256-253.55H383.511c-172.849 0-312.967 140.12-312.967 312.967 0 112.509 59.367 211.151 148.483 266.31 38.117 23.594 22.226 179.433 22.226 179.433s186.946-132.776 199.159-132.776h227.613c172.849 0 312.967-140.12 312.967-312.967S840.874 150.051 668.025 150.051z m0.387 585.628H433.059c-10.721 0-153.872 97.21-153.872 97.21s-6.404-118.311-40.405-138.034c-71.3-41.359-129.705-145.439-130.304-233.022-0.967-141.385 132.829-272.858 274.645-273.846h285.29c137.871 0 274.647 136.418 274.647 273.846-0.001 144.334-135.791 275.821-274.648 273.846z m84.968-332.078c-43.565 0.395-56.901 16.984-56.901 37.934 0 20.952 15.113 37.935 56.901 37.935 41.79 0 56.903-16.984 56.903-37.935s-13.336-38.331-56.903-37.934z" fill="#F74A82"/>
        </svg>
      </div>
    </velt-comment-tool-wireframe>

    <!-- Replaced Comment Pin with custom pin -->
    <velt-comment-pin-wireframe>
      <div class="comment-pin">
        <svg xmlns="http://www.w3.org/2000/svg" width="40px" height="40px" viewBox="0 0 64 64" fill="none">
          <path d="M56.24 21.827L41.72 7.31104C41.2715 6.86093 40.7302 6.51413 40.1339 6.29485C39.5375 6.07557 38.9005 5.9891 38.2672 6.04147C37.634 6.09384 37.0198 6.2838 36.4676 6.59807C35.9154 6.91235 35.4384 7.34337 35.07 7.86104L22.11 26.051C22.0751 26.0984 22.0301 26.1374 21.9781 26.1651C21.9262 26.1928 21.8688 26.2085 21.81 26.211L16.24 26.251C15.3787 26.258 14.5386 26.5194 13.8255 27.0024C13.1124 27.4855 12.558 28.1686 12.232 28.9659C11.906 29.7632 11.8231 30.639 11.9935 31.4833C12.164 32.3276 12.5803 33.1027 13.19 33.711L20.1 40.621L22.93 43.451L29.84 50.361C30.4484 50.9708 31.2234 51.3871 32.0677 51.5575C32.912 51.728 33.7879 51.645 34.5852 51.319C35.3824 50.9931 36.0655 50.4387 36.5486 49.7255C37.0316 49.0124 37.2931 48.1724 37.3 47.311L37.34 41.741C37.3426 41.6823 37.3583 41.6248 37.386 41.5729C37.4137 41.521 37.4526 41.4759 37.5 41.441L55.69 28.481C56.207 28.1113 56.6375 27.6336 56.9517 27.0811C57.266 26.5286 57.4565 25.9144 57.51 25.281C57.5656 24.6473 57.4805 24.0092 57.261 23.4121C57.0415 22.8151 56.6928 22.2738 56.24 21.827Z" fill="#ffabc6"/>
          <path d="M22.93 43.451L8.94 57.441C8.56472 57.8163 8.05572 58.0271 7.52499 58.0271C6.99427 58.0271 6.48527 57.8163 6.10999 57.441C5.7347 57.0657 5.5239 56.5567 5.5239 56.026C5.5239 55.4952 5.7347 54.9863 6.10999 54.611L20.1 40.621L22.93 43.451Z" fill="#F74A82"/>
        </svg>
      </div>
    </velt-comment-pin-wireframe>
  </velt-wireframe>
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

<style>
/**
* To customize the Velt comment dialog styles
*/
body {
  --velt-comment-pin-highlight: 2px dashed #F74A82;
}

velt-wireframe {
  display: none;
}

.comment-tool, .comment-pin {
  cursor: pointer;
}

.comment-dialog-container {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.modal-div {
  border-radius: 4px !important;
  border: 0.75px solid #FC48773D !important;
}

.modal-div.no-comments {
  border-radius: 12px !important;
  border: 2px solid #F74A8229 !important;
}

.modal-div.bottom-sheet {
  border-bottom-left-radius: 0 !important;
  border-bottom-right-radius: 0 !important;
}

.modal-div .velt-composer--input-button {
  background-color: #F74A82 !important;
}

.modal-div .dropdown-container .v-dropdown-menu-trigger {
  padding: 4px 6px 4px 8px;
}
</style>
