<script setup>
import { onMounted } from "vue";

import { initVelt } from "@veltdev/client";

let client;

const initializeVelt = async () => {
  // Initialize the Velt client with your API key
  console.log("Initializing Velt");
  client = await initVelt("j3AwoBkuQMTEgeqrmPve");
};

/**
 * To set the document ID for the Velt client
 */
const setDocumentId = () => {
  if (client) {
    console.log("Setting document ID");
    client.setDocumentId("vue-3-example");
  }
};

/**
 * To identify the user for the Velt client
 */
const identifyUser = () => {
  if (client) {
    // Replace the user object with your user data
    const user = {
      userId: "user1",
      email: "user1@velt.dev",
      name: "User 1",
      color: "#8b4bef",
      organizationId: "testOrg1",
    };
    console.log("Identifying user");
    client.identify(user);
  }
};

const handleSidebarCommentClick = () => {
  console.log("Comment Clicked on Sidebar");
  const veltCommentsSidebar = document.querySelector("velt-comments-sidebar");
  veltCommentsSidebar?.addEventListener("onCommentClick", (event) => {
    console.log("onCommentClick:", event.detail);
  });
};

const setCustomReactions = () => {
  console.log("Setting custom reactions");
  const commentElement = client?.getCommentElement();
  if (commentElement) {
    const reactionMap = {
      RAISED_HANDS: {
        emoji: "🙌",
      },
      THUMBS_DOWN: {
        emoji: "👎",
      },
      THUMBS_UP: {
        emoji: "👍",
      },
      HEART_FACE: {
        emoji: "💖",
      },
      TEARS_OF_JOY: {
        emoji: "😂",
      },
      EYES: {
        emoji: "👀",
      },
      FIRE: {
        emoji: "🔥",
      },
    };

    commentElement.setCustomReactions(reactionMap);
  }
};

/**
 * To enable comments on specific elements
 */
const setAllowedElementIds = () => {
  if (client) {
    const commentElement = client.getCommentElement();
    commentElement.allowedElementIds(["canvas"]);
  }
};

onMounted(async () => {
  // Call the initializeVelt function when the component is mounted
  await initializeVelt();
  setDocumentId();
  identifyUser();
	setAllowedElementIds();
  setCustomReactions();
  handleSidebarCommentClick();
});
</script>

<template>
  <velt-comments comment-pin-highlighter="true"></velt-comments>
  <velt-comments-sidebar></velt-comments-sidebar>

  <div class="recent-dashboard-viewers">
    <h2>Email Template Builder</h2>
    <div class="viewers-tools">
      <velt-presence></velt-presence>
      <velt-comment-tool></velt-comment-tool>
      <velt-sidebar-button></velt-sidebar-button>
    </div>
  </div>

  <div class="email-builder">
    <div class="template-sidebar" id="sidebar">
      <h3>Components</h3>
      <div class="component-list">
        <button class="component-btn">Header</button>
        <button class="component-btn">Text Block</button>
        <button class="component-btn">Image</button>
        <button class="component-btn">Button</button>
        <button class="component-btn">Divider</button>
      </div>
    </div>

    <div class="template-canvas" id="canvas">
      <div class="email-container" id="dynamic-block">
        <div class="email-header">
          <input
            type="text"
            placeholder="Email Subject"
            class="subject-input"
          />
        </div>
        <div class="email-body">
          <div class="placeholder-text">
            Drag and drop components here to build your email
          </div>
        </div>
      </div>
    </div>
  </div>

  <velt-wireframe style="display: none;">
	<velt-comment-dialog-status-wireframe velt-if="false">
	</velt-comment-dialog-status-wireframe>

	<velt-comment-dialog-composer-action-button-wireframe type="attachments" velt-if="false">
	</velt-comment-dialog-composer-action-button-wireframe>

	<velt-comment-dialog-composer-action-button-wireframe type="audio" velt-if="false">
	</velt-comment-dialog-composer-action-button-wireframe>

	<velt-comment-dialog-composer-action-button-wireframe type="video" velt-if="false">
	</velt-comment-dialog-composer-action-button-wireframe>

	<velt-comment-dialog-composer-action-button-wireframe type="screen" velt-if="false">
	</velt-comment-dialog-composer-action-button-wireframe>

	</velt-wireframe>
</template>

<style scoped>
p {
  margin: 0;
}

h2 {
  margin: 0;
}

h3 {
  margin: 0;
}

.marked-as-resolved {
  display: flex;
  align-items: center;
  padding-bottom: 10px;
  margin-bottom: 10px;
  border-bottom: 1px solid #ccc;
  gap: 8px;
}

.recent-dashboard-viewers {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 32px 16px;
  box-sizing: border-box;
}

.viewers-tools {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.email-builder {
  display: flex;
  gap: 24px;
  padding: 32px;
  height: calc(100vh - 200px);
}

.template-sidebar {
  width: 250px;
  background: var(--velt-light-mode-background-2);
  border-radius: 8px;
  padding: 16px;
}

.component-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-top: 16px;
}

.component-btn {
  padding: 12px;
  background: white;
  border: 1px solid var(--velt-light-mode-border-5);
  border-radius: 6px;
  cursor: pointer;
  text-align: left;
  transition: all 0.2s;
}

.component-btn:hover {
  background: var(--velt-light-mode-background-3);
}

.template-canvas {
  flex: 1;
  background: var(--velt-light-mode-background-2);
  border-radius: 8px;
  padding: 24px;
  overflow-y: auto;
}

.email-container {
  max-width: 600px;
  margin: 0 auto;
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.email-header {
  padding: 24px;
  border-bottom: 1px solid var(--velt-light-mode-border-5);
}

.subject-input {
  width: 100%;
  padding: 8px;
  border: 1px solid var(--velt-light-mode-border-5);
  border-radius: 4px;
  font-size: 16px;
}

.email-body {
  min-height: 400px;
  padding: 24px;
}

.placeholder-text {
  color: var(--velt-light-mode-text-10);
  text-align: center;
  padding: 40px;
  border: 2px dashed var(--velt-light-mode-border-5);
  border-radius: 8px;
}

/* Velt Theme Configuration */

/* Border Radius */
--velt-border-radius-2xs: 1.5px;
--velt-border-radius-xs: 3px;
--velt-border-radius-sm: 6px;
--velt-border-radius-md: 9px;
--velt-border-radius-lg: 12px;
--velt-border-radius-xl: 15px;
--velt-border-radius-2xl: 18px;
--velt-border-radius-3xl: 24px;
--velt-border-radius-full: 60px;

/* Light Mode */
/* Accent Colors */
--velt-light-mode-accent: #2569de;
--velt-light-mode-accent-text: #2569de;
--velt-light-mode-accent-hover: #0036ab;
--velt-light-mode-accent-foreground: #ffffff;
--velt-light-mode-accent-light: #f4f8fd;
--velt-light-mode-accent-transparent: rgba(37, 105, 222, 0.08);

/* Background Shades */
--velt-light-mode-background-0: #ffffff;
--velt-light-mode-background-1: #fcfcfc;
--velt-light-mode-background-2: #fafafa;
--velt-light-mode-background-3: #f7f7f7;
--velt-light-mode-background-4: #f5f5f5;
--velt-light-mode-background-5: #f2f2f2;
--velt-light-mode-background-6: #f0f0f0;
--velt-light-mode-background-7: #ededed;
--velt-light-mode-background-8: #ebebeb;
--velt-light-mode-background-9: #e8e8e8;
--velt-light-mode-background-10: #e6e6e6;

/* Text Shades */
--velt-light-mode-text-0: #0a0a0a;
--velt-light-mode-text-1: #171717;
--velt-light-mode-text-2: #242424;
--velt-light-mode-text-3: #303030;
--velt-light-mode-text-4: #3d3d3d;
--velt-light-mode-text-5: #4a4a4a;
--velt-light-mode-text-6: #575757;
--velt-light-mode-text-7: #636363;
--velt-light-mode-text-8: #707070;
--velt-light-mode-text-9: #7d7d7d;
--velt-light-mode-text-10: #898989;
--velt-light-mode-text-11: #969696;
--velt-light-mode-text-12: #a3a3a3;

/* Border Shades */
--velt-light-mode-border-0: #ffffff;
--velt-light-mode-border-1: #fafafa;
--velt-light-mode-border-2: #f5f5f5;
--velt-light-mode-border-3: #f0f0f0;
--velt-light-mode-border-4: #ebebeb;
--velt-light-mode-border-5: #e5e5e5;
--velt-light-mode-border-6: #e0e0e0;
--velt-light-mode-border-7: #dbdbdb;
--velt-light-mode-border-8: #d6d6d6;
--velt-light-mode-border-9: #d1d1d1;
--velt-light-mode-border-10: #cccccc;

/* Semantic Colors */
--velt-light-mode-error: #ff7162;
--velt-light-mode-error-hover: #de5041;
--velt-light-mode-error-foreground: #ffffff;
--velt-light-mode-error-light: #fff4f2;
--velt-light-mode-warning: #ffcd2e;
--velt-light-mode-warning-hover: #c69400;
--velt-light-mode-warning-foreground: #474747;
--velt-light-mode-warning-light: #fffbee;
--velt-light-mode-success: #198f65;
--velt-light-mode-success-hover: #006b41;
--velt-light-mode-success-foreground: #ffffff;
--velt-light-mode-success-light: #edf6f3;

/* Dark Mode */
/* Accent Colors */
--velt-dark-mode-accent: #2569de;
--velt-dark-mode-accent-text: #9ab8eb;
--velt-dark-mode-accent-hover: #0036ab;
--velt-dark-mode-accent-foreground: #ffffff;
--velt-dark-mode-accent-light: #f4f8fd;
--velt-dark-mode-accent-transparent: rgba(37, 105, 222, 0.08);

/* Background Shades */
--velt-dark-mode-background-0: #000000;
--velt-dark-mode-background-1: #030303;
--velt-dark-mode-background-2: #050505;
--velt-dark-mode-background-3: #080808;
--velt-dark-mode-background-4: #0a0a0a;
--velt-dark-mode-background-5: #0d0d0d;
--velt-dark-mode-background-6: #0f0f0f;
--velt-dark-mode-background-7: #121212;
--velt-dark-mode-background-8: #141414;
--velt-dark-mode-background-9: #171717;
--velt-dark-mode-background-10: #1a1a1a;

/* Text Shades */
--velt-dark-mode-text-0: #ffffff;
--velt-dark-mode-text-1: #f2f2f2;
--velt-dark-mode-text-2: #e6e6e6;
--velt-dark-mode-text-3: #d9d9d9;
--velt-dark-mode-text-4: #cccccc;
--velt-dark-mode-text-5: #bfbfbf;
--velt-dark-mode-text-6: #b3b3b3;
--velt-dark-mode-text-7: #a6a6a6;
--velt-dark-mode-text-8: #999999;
--velt-dark-mode-text-9: #8c8c8c;
--velt-dark-mode-text-10: #808080;
--velt-dark-mode-text-11: #737373;
--velt-dark-mode-text-12: #666666;

/* Border Shades */
--velt-dark-mode-border-0: #0f0f0f;
--velt-dark-mode-border-1: #1a1a1a;
--velt-dark-mode-border-2: #1f1f1f;
--velt-dark-mode-border-3: #242424;
--velt-dark-mode-border-4: #292929;
--velt-dark-mode-border-5: #2e2e2e;
--velt-dark-mode-border-6: #333333;
--velt-dark-mode-border-7: #383838;
--velt-dark-mode-border-8: #3d3d3d;
--velt-dark-mode-border-9: #424242;
--velt-dark-mode-border-10: #474747;

/* Semantic Colors */
--velt-dark-mode-error: #ff7162;
--velt-dark-mode-error-hover: #de5041;
--velt-dark-mode-error-foreground: #ffffff;
--velt-dark-mode-error-light: #fff4f2;
--velt-dark-mode-warning: #ffcd2e;
--velt-dark-mode-warning-hover: #c69400;
--velt-dark-mode-warning-foreground: #474747;
--velt-dark-mode-warning-light: #fffbee;
--velt-dark-mode-success: #198f65;
--velt-dark-mode-success-hover: #006b41;
--velt-dark-mode-success-foreground: #ffffff;
--velt-dark-mode-success-light: #edf6f3;

/* Spacing */
--velt-spacing-2xs: 0.09375rem;
--velt-spacing-xs: 0.1875rem;
--velt-spacing-sm: 0.375rem;
--velt-spacing-md: 0.5625rem;
--velt-spacing-lg: 0.75rem;
--velt-spacing-xl: 0.9375rem;
--velt-spacing-2xl: 1.125rem;

/* Font Size */
--velt-font-size-2xs: 0.625rem;
--velt-font-size-xs: 0.75rem;
--velt-font-size-sm: 0.875rem;
--velt-font-size-md: 1rem;
--velt-font-size-lg: 1.5rem;
--velt-font-size-xl: 1.75rem;
--velt-font-size-2xl: 2rem;
</style>
