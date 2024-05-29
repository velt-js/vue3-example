<script setup>
import { onMounted } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

import { initVelt } from '@veltdev/client'

let client;

const initializeVelt = async () => {
	// Initialize the Velt client with your API key
	client = await initVelt("hny91vx3KUxEIp61jBd1");
}

/**
 * To set the document ID for the Velt client
 */
const setDocumentId = () => {
	if (client) {
		client.setDocumentId("pendo-velt-integration-customization");
	}
}

/**
 * To identify the user for the Velt client
 */
const identifyUser = () => {
	if (client) {
		// Replace the user object with your user data
		const user = {
			userId: "1",
			email: "test@velt.dev",
			name: "Test User",
			color: "#8b4bef",
		};
		client.identify(user);
	}
}

const handleSidebarCommentClick = () => {
	const veltCommentsSidebar = document.querySelector('velt-comments-sidebar');
	veltCommentsSidebar?.addEventListener('onCommentClick', (event) => {
		console.log('onCommentClick:', event.detail);
	});
}

const setCustomReactions = () => {
	const commentElement = client?.getCommentElement();
	if (commentElement) {
		const reactionMap = {
			RAISED_HANDS: {
				url: 'https://em-content.zobj.net/source/telegram/386/raising-hands_1f64c.webp'
			},
			THUMBS_DOWN: {
				url: 'https://em-content.zobj.net/source/telegram/386/thumbs-down_1f44e.webp',
			},
			THUMBS_UP: {
				url: 'https://em-content.zobj.net/source/telegram/386/thumbs-up_1f44d.webp',
			},
			HEART_FACE: {
				url: 'https://em-content.zobj.net/source/telegram/386/smiling-face-with-hearts_1f970.webp',
			},
			TEARS_OF_JOY: {
				url: 'https://em-content.zobj.net/source/telegram/386/face-with-tears-of-joy_1f602.webp',
			},
			EYES: {
				url: 'https://em-content.zobj.net/source/telegram/386/eyes_1f440.webp',
			},
			FIRE: {
				url: 'https://em-content.zobj.net/source/telegram/386/fire_1f525.webp',
			}
		};

		commentElement.setCustomReactions(reactionMap);
	}
}

onMounted(async () => {
	// Call the initializeVelt function when the component is mounted
	await initializeVelt();
	setDocumentId();
	identifyUser();
	setCustomReactions();
	handleSidebarCommentClick();
});
</script>

<template>
	<velt-comments resolved-comments-on-dom="true" popover-mode="true" shadow-dom="false" dialog-shadow-dom=”false”
		popover-triangle-component="false"></velt-comments>
	<velt-comments-sidebar shadow-dom="false"></velt-comments-sidebar>

	<div class="recent-dashboard-viewers">
		<h2>Pendo Velt Integration (customization)</h2>
		<div class="viewers-tools">
			<velt-presence></velt-presence>
			<velt-sidebar-button></velt-sidebar-button>
		</div>

	</div>

	<div class="support-page">

		<div class="bubble-comment-container" id="dynamic-block">
			<div class="header">
				<p>Reports run over time</p>
				<div class="viewers-tools">
					<velt-comment-bubble target-comment-element-id="dynamic-block"></velt-comment-bubble>
					<velt-comment-tool target-comment-element-id="dynamic-block"></velt-comment-tool>
				</div>
			</div>
			<div class="body"></div>
		</div>

		<div class="bubble-comment-container" id="dynamic-block-2">
			<div class="header">
				<p>Reports run over time</p>
				<div class="viewers-tools">
					<velt-comment-bubble target-comment-element-id="dynamic-block-2"></velt-comment-bubble>
					<velt-comment-tool target-comment-element-id="dynamic-block-2"></velt-comment-tool>
				</div>
			</div>
			<div class="body"></div>
		</div>

		<div class="bubble-comment-container" id="dynamic-block-3">
			<div class="header">
				<p>Reports run over time</p>
				<div class="viewers-tools">
					<velt-comment-bubble target-comment-element-id="dynamic-block-3"></velt-comment-bubble>
					<velt-comment-tool target-comment-element-id="dynamic-block-3"></velt-comment-tool>
				</div>
			</div>
			<div class="body"></div>
		</div>

		<div class="bubble-comment-container" id="dynamic-block-4">
			<div class="header">
				<p>Reports run over time</p>
				<div class="viewers-tools">
					<velt-comment-bubble target-comment-element-id="dynamic-block-4"></velt-comment-bubble>
					<velt-comment-tool target-comment-element-id="dynamic-block-4"></velt-comment-tool>
				</div>
			</div>
			<div class="body"></div>
		</div>

	</div>

	<velt-wireframe style="display:none;">
		<velt-comment-tool-wireframe>
			<div class="custom-bubble-tool">
				<svg width="25" height="25" viewBox="0 0 25 25" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path fill-rule="evenodd" clip-rule="evenodd"
						d="M12.6056 22.2012C18.4045 22.2012 23.1056 17.5002 23.1056 11.7012C23.1056 5.90218 18.4045 1.20117 12.6056 1.20117C6.80657 1.20117 2.10556 5.90218 2.10556 11.7012C2.10556 13.615 2.61759 15.4093 3.51215 16.9544C3.61668 17.135 3.62814 17.356 3.53484 17.5426L1.26545 22.0814C1.02471 22.5629 1.49078 23.0933 1.99921 22.9164L7.44805 21.0212C7.47568 21.0116 7.48497 20.9772 7.46593 20.9549C7.43544 20.9194 7.47892 20.8668 7.51989 20.8896C9.0266 21.7253 10.7605 22.2012 12.6056 22.2012Z"
						fill="#3290A7" />
					<path
						d="M7.51989 20.8896L8.10195 19.8402L7.51989 20.8896ZM7.44805 21.0212L7.84227 22.1546L7.44805 21.0212ZM1.26545 22.0814L2.33876 22.6181L1.26545 22.0814ZM1.99921 22.9164L2.39344 24.0498L1.99921 22.9164ZM3.51215 16.9544L2.47364 17.5557L3.51215 16.9544ZM3.53484 17.5426L2.46153 17.006L3.53484 17.5426ZM21.9056 11.7012C21.9056 16.8374 17.7418 21.0012 12.6056 21.0012V23.4012C19.0673 23.4012 24.3056 18.1629 24.3056 11.7012H21.9056ZM12.6056 2.40117C17.7418 2.40117 21.9056 6.56492 21.9056 11.7012H24.3056C24.3056 5.23944 19.0673 0.00117183 12.6056 0.00117183V2.40117ZM3.30556 11.7012C3.30556 6.56492 7.46931 2.40117 12.6056 2.40117V0.00117183C6.14383 0.00117183 0.905557 5.23944 0.905557 11.7012H3.30556ZM4.55066 16.3532C3.75905 14.9858 3.30556 13.3983 3.30556 11.7012H0.905557C0.905557 13.8318 1.47614 15.8327 2.47364 17.5557L4.55066 16.3532ZM2.33876 22.6181L4.60815 18.0793L2.46153 17.006L0.192132 21.5447L2.33876 22.6181ZM7.05382 19.8878L1.60499 21.783L2.39344 24.0498L7.84227 22.1546L7.05382 19.8878ZM12.6056 21.0012C10.9693 21.0012 9.43512 20.5796 8.10195 19.8402L6.93783 21.9389C8.61807 22.8709 10.5517 23.4012 12.6056 23.4012V21.0012ZM8.37704 20.174C8.81244 20.682 8.67692 21.3189 8.39118 21.6647C8.107 22.0087 7.51533 22.2593 6.93783 21.9389L8.10195 19.8402C7.48347 19.4971 6.84959 19.7626 6.54104 20.136C6.23095 20.5113 6.08893 21.1924 6.55482 21.7359L8.37704 20.174ZM7.84227 22.1546C8.66854 21.8672 8.94637 20.8382 8.37704 20.174L6.55482 21.7359C6.02357 21.1161 6.28282 20.156 7.05382 19.8878L7.84227 22.1546ZM0.192132 21.5447C-0.530083 22.9892 0.868146 24.5804 2.39344 24.0498L1.60499 21.783C2.11342 21.6062 2.5795 22.1366 2.33876 22.6181L0.192132 21.5447ZM2.47364 17.5557C2.38662 17.4054 2.36499 17.199 2.46153 17.006L4.60815 18.0793C4.89129 17.513 4.84674 16.8646 4.55066 16.3532L2.47364 17.5557Z"
						fill="#036479" />
				</svg>
			</div>
		</velt-comment-tool-wireframe>
		<velt-comment-status type="resolved">

		</velt-comment-status>
		<velt-comment-bubble-wireframe>
			<div class="custom-bubble-tool">
				<svg width="25" height="25" viewBox="0 0 25 25" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path fill-rule="evenodd" clip-rule="evenodd"
						d="M12.6056 22.2012C18.4045 22.2012 23.1056 17.5002 23.1056 11.7012C23.1056 5.90218 18.4045 1.20117 12.6056 1.20117C6.80657 1.20117 2.10556 5.90218 2.10556 11.7012C2.10556 13.615 2.61759 15.4093 3.51215 16.9544C3.61668 17.135 3.62814 17.356 3.53484 17.5426L1.26545 22.0814C1.02471 22.5629 1.49078 23.0933 1.99921 22.9164L7.44805 21.0212C7.47568 21.0116 7.48497 20.9772 7.46593 20.9549C7.43544 20.9194 7.47892 20.8668 7.51989 20.8896C9.0266 21.7253 10.7605 22.2012 12.6056 22.2012Z"
						fill="#3290A7" />
					<path
						d="M7.51989 20.8896L8.10195 19.8402L7.51989 20.8896ZM7.44805 21.0212L7.84227 22.1546L7.44805 21.0212ZM1.26545 22.0814L2.33876 22.6181L1.26545 22.0814ZM1.99921 22.9164L2.39344 24.0498L1.99921 22.9164ZM3.51215 16.9544L2.47364 17.5557L3.51215 16.9544ZM3.53484 17.5426L2.46153 17.006L3.53484 17.5426ZM21.9056 11.7012C21.9056 16.8374 17.7418 21.0012 12.6056 21.0012V23.4012C19.0673 23.4012 24.3056 18.1629 24.3056 11.7012H21.9056ZM12.6056 2.40117C17.7418 2.40117 21.9056 6.56492 21.9056 11.7012H24.3056C24.3056 5.23944 19.0673 0.00117183 12.6056 0.00117183V2.40117ZM3.30556 11.7012C3.30556 6.56492 7.46931 2.40117 12.6056 2.40117V0.00117183C6.14383 0.00117183 0.905557 5.23944 0.905557 11.7012H3.30556ZM4.55066 16.3532C3.75905 14.9858 3.30556 13.3983 3.30556 11.7012H0.905557C0.905557 13.8318 1.47614 15.8327 2.47364 17.5557L4.55066 16.3532ZM2.33876 22.6181L4.60815 18.0793L2.46153 17.006L0.192132 21.5447L2.33876 22.6181ZM7.05382 19.8878L1.60499 21.783L2.39344 24.0498L7.84227 22.1546L7.05382 19.8878ZM12.6056 21.0012C10.9693 21.0012 9.43512 20.5796 8.10195 19.8402L6.93783 21.9389C8.61807 22.8709 10.5517 23.4012 12.6056 23.4012V21.0012ZM8.37704 20.174C8.81244 20.682 8.67692 21.3189 8.39118 21.6647C8.107 22.0087 7.51533 22.2593 6.93783 21.9389L8.10195 19.8402C7.48347 19.4971 6.84959 19.7626 6.54104 20.136C6.23095 20.5113 6.08893 21.1924 6.55482 21.7359L8.37704 20.174ZM7.84227 22.1546C8.66854 21.8672 8.94637 20.8382 8.37704 20.174L6.55482 21.7359C6.02357 21.1161 6.28282 20.156 7.05382 19.8878L7.84227 22.1546ZM0.192132 21.5447C-0.530083 22.9892 0.868146 24.5804 2.39344 24.0498L1.60499 21.783C2.11342 21.6062 2.5795 22.1366 2.33876 22.6181L0.192132 21.5447ZM2.47364 17.5557C2.38662 17.4054 2.36499 17.199 2.46153 17.006L4.60815 18.0793C4.89129 17.513 4.84674 16.8646 4.55066 16.3532L2.47364 17.5557Z"
						fill="#036479" />
				</svg>
				<velt-comment-bubble-comments-count-wireframe></velt-comment-bubble-comments-count-wireframe>
			</div>
		</velt-comment-bubble-wireframe>

		<velt-comment-dialog-wireframe>
			<div class="marked-as-resolved">
				<svg width="18" height="18" viewBox="0 0 24 24" fill="#0DCF82" xmlns="http://www.w3.org/2000/svg">
					<path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z"
						stroke="#0DCF82" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
					<path d="M7.75 11.9999L10.58 14.8299L16.25 9.16992" stroke="white" stroke-width="1.5"
						stroke-linecap="round" stroke-linejoin="round" />
				</svg>
				<p>Marked as resolved</p>
			</div>
			<velt-comment-dialog-body-wireframe>
				<velt-comment-dialog-threads-wireframe>
					<velt-comment-dialog-thread-card-wireframe>
						<div class="thread-card-header">
							<div class="thread-card-header-left">
								<div class="thread-card-header-avatar-container">
									<velt-comment-dialog-thread-card-avatar-wireframe></velt-comment-dialog-thread-card-avatar-wireframe>
								</div>
								<velt-comment-dialog-thread-card-name-wireframe></velt-comment-dialog-thread-card-name-wireframe>
								<velt-comment-dialog-thread-card-time-wireframe></velt-comment-dialog-thread-card-time-wireframe>
							</div>

							<velt-comment-dialog-thread-card-options-wireframe>
								<velt-comment-dialog-options-dropdown-content-wireframe>
									<div class="resolve-button" id="resolveButton">
										<velt-comment-dialog-resolve-button-wireframe>
											<p class="option-item">Resolve</p>
										</velt-comment-dialog-resolve-button-wireframe>
									</div>
									<velt-comment-dialog-options-dropdown-content-edit-wireframe>
										<p class="option-item">Edit</p>
									</velt-comment-dialog-options-dropdown-content-edit-wireframe>
									<velt-comment-dialog-options-dropdown-content-delete-wireframe>
										<p class="option-item">Delete</p>
									</velt-comment-dialog-options-dropdown-content-delete-wireframe>
								</velt-comment-dialog-options-dropdown-content-wireframe>
							</velt-comment-dialog-thread-card-options-wireframe>
						</div>
						<velt-comment-dialog-thread-card-message-wireframe></velt-comment-dialog-thread-card-message-wireframe>
						<velt-comment-dialog-thread-card-reactions-wireframe></velt-comment-dialog-thread-card-reactions-wireframe>
					</velt-comment-dialog-thread-card-wireframe>
					<velt-comment-dialog-more-reply-wireframe></velt-comment-dialog-more-reply-wireframe>
				</velt-comment-dialog-threads-wireframe>
				<velt-comment-dialog-toggle-reply-wireframe></velt-comment-dialog-toggle-reply-wireframe>
			</velt-comment-dialog-body-wireframe>
			<!-- Composer -->
			<velt-comment-dialog-composer-wireframe>
				<div class="first-message">
					<h3>Start a conversion</h3>
					<p>Ask a question, give a feedback, or just say "Hi". Anyone who can access this page in Pendo can
						view and
						adds comments here.
					</p>
				</div>
				<div class="composer-box">
					<velt-comment-dialog-composer-input-wireframe></velt-comment-dialog-composer-input-wireframe>
					<div class="composer-box-actions">
						<velt-comment-dialog-composer-action-button-wireframe
							type="userMentions"></velt-comment-dialog-composer-action-button-wireframe>

						<velt-comment-dialog-composer-assign-user-wireframe></velt-comment-dialog-composer-assign-user-wireframe>
						<velt-comment-dialog-composer-action-button-wireframe type="submit">
							<div class="submit-button">
								<svg width="16" height="10" viewBox="0 0 16 10" fill="none"
									xmlns="http://www.w3.org/2000/svg">
									<path d="M1 5H15M15 5L11 9M15 5L11 1" stroke="white" stroke-width="1.25"
										stroke-linecap="round" stroke-linejoin="round" />
								</svg>
							</div>
						</velt-comment-dialog-composer-action-button-wireframe>
					</div>
				</div>
			</velt-comment-dialog-composer-wireframe>
		</velt-comment-dialog-wireframe>

		<velt-reaction-tool-wireframe>
			<svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
				<path
					d="M15.75 9C15.75 9.88642 15.5754 10.7642 15.2362 11.5831C14.897 12.4021 14.3998 13.1462 13.773 13.773C13.1462 14.3998 12.4021 14.897 11.5831 15.2362C10.7642 15.5754 9.88642 15.75 9 15.75C8.11358 15.75 7.23583 15.5754 6.41689 15.2362C5.59794 14.897 4.85382 14.3998 4.22703 13.773C3.60023 13.1462 3.10303 12.4021 2.76381 11.5831C2.42459 10.7642 2.25 9.88642 2.25 9C2.25 8.11358 2.42459 7.23583 2.76381 6.41689C3.10303 5.59794 3.60023 4.85382 4.22703 4.22703C4.85382 3.60023 5.59794 3.10303 6.41689 2.76381C7.23583 2.42459 8.11358 2.25 9 2.25C9.88642 2.25 10.7642 2.42459 11.5831 2.76381M6.75 7.5H6.7575M11.25 7.5H11.2575M7.125 11.25C7.36941 11.4994 7.66114 11.6976 7.9831 11.8329C8.30505 11.9682 8.65077 12.0379 9 12.0379C9.34923 12.0379 9.69495 11.9682 10.0169 11.8329C10.3389 11.6976 10.6306 11.4994 10.875 11.25M12.25 5.01322H16.75M14.5 2.76322V7.26322"
					stroke="#2A2C34" stroke-width="1.25" stroke-linecap="round" stroke-linejoin="round" />
			</svg>
		</velt-reaction-tool-wireframe>

		<velt-sidebar-button-wireframe>
			<div class="custom-sidebar-button">
				<svg width="12" height="12" viewBox="0 0 25 25" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path
						d="M7.51989 20.8896L8.10195 19.8402L7.51989 20.8896ZM7.44805 21.0212L7.84227 22.1546L7.44805 21.0212ZM1.26545 22.0814L2.33876 22.6181L1.26545 22.0814ZM1.99921 22.9164L2.39344 24.0498L1.99921 22.9164ZM3.51215 16.9544L2.47364 17.5557L3.51215 16.9544ZM3.53484 17.5426L2.46153 17.006L3.53484 17.5426ZM21.9056 11.7012C21.9056 16.8374 17.7418 21.0012 12.6056 21.0012V23.4012C19.0673 23.4012 24.3056 18.1629 24.3056 11.7012H21.9056ZM12.6056 2.40117C17.7418 2.40117 21.9056 6.56492 21.9056 11.7012H24.3056C24.3056 5.23944 19.0673 0.00117183 12.6056 0.00117183V2.40117ZM3.30556 11.7012C3.30556 6.56492 7.46931 2.40117 12.6056 2.40117V0.00117183C6.14382 0.00117183 0.905557 5.23944 0.905557 11.7012H3.30556ZM4.55066 16.3532C3.75905 14.9858 3.30556 13.3983 3.30556 11.7012H0.905557C0.905557 13.8318 1.47614 15.8327 2.47364 17.5557L4.55066 16.3532ZM2.33876 22.6181L4.60815 18.0793L2.46153 17.006L0.192132 21.5447L2.33876 22.6181ZM7.05382 19.8878L1.60499 21.783L2.39344 24.0498L7.84227 22.1546L7.05382 19.8878ZM12.6056 21.0012C10.9693 21.0012 9.43512 20.5796 8.10195 19.8402L6.93783 21.9389C8.61807 22.8709 10.5517 23.4012 12.6056 23.4012V21.0012ZM8.37704 20.174C8.81244 20.682 8.67692 21.3189 8.39119 21.6647C8.107 22.0087 7.51533 22.2593 6.93783 21.9389L8.10195 19.8402C7.48347 19.4971 6.84959 19.7626 6.54104 20.136C6.23095 20.5113 6.08893 21.1923 6.55482 21.7359L8.37704 20.174ZM7.84227 22.1546C8.66854 21.8672 8.94637 20.8382 8.37704 20.174L6.55482 21.7359C6.02357 21.1161 6.28282 20.156 7.05382 19.8878L7.84227 22.1546ZM0.192132 21.5447C-0.530083 22.9892 0.868146 24.5804 2.39344 24.0498L1.60499 21.783C2.11342 21.6062 2.5795 22.1366 2.33876 22.6181L0.192132 21.5447ZM2.47364 17.5557C2.38662 17.4054 2.36499 17.199 2.46153 17.006L4.60815 18.0793C4.89129 17.513 4.84674 16.8646 4.55066 16.3532L2.47364 17.5557Z"
						fill="#036479" />
				</svg>
			</div>
		</velt-sidebar-button-wireframe>
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

.support-page {
	align-items: center;
	justify-content: center;
	display: flex;
	flex-direction: column;
	gap: 32px;
	padding-block: 64px;
	padding-inline: 30%;
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

.bubble-comment-container {
	width: 100%;

	.header {
		border: 1px solid #ccc;
		padding: 16px;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		box-sizing: border-box;
	}

	.body {
		box-sizing: border-box;
		width: 100%;
		border: 1px solid #ccc;
		border-top-width: 0px;
		background-color: aliceblue;
		height: 300px;
	}
}

.custom-bubble-tool {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 4px;

	app-comment-bubble-comments-count {
		color: #036479;
		font-weight: bold;
		font-size: 16px;
	}
}

.thread-card-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 8px;

	.thread-card-header-left {
		display: flex;
		align-items: center;
		gap: 8px;


		.placeholder-avatar {
			width: 20px;
			height: 20px;
			border-radius: 50%;
			background-color: rgb(139, 75, 239);
			color: white;
			display: flex;
			align-items: center;
			justify-content: center;
			font-size: 12px;
		}
	}
}

.composer-box {
	margin-top: 16px;
	border: 1px solid #ccc;
	padding: 2px;
	width: 100%;
	box-sizing: border-box;
	border-radius: 4px;

	.composer-box-actions {
		border-top: 1px solid #cccccca2;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding-top: 4px;

		.submit-button {
			padding: 8px;
			display: flex;
			align-items: center;
			justify-content: center;
			border-radius: 4px;
			background-color: #3290A7;
		}

	}
}

.first-message {
	display: none;
	flex-direction: column;
	gap: 4px;
	padding: 8px;
}

.custom-sidebar-button {
	padding: 8px;
	border-radius: 4px;
	border: 1px solid #036479;
	display: flex;
	cursor: pointer;
}

.resolve-button {
	width: 100%;
}

.option-item {
	width: 100% !important;
	padding-inline: 8px !important;
	padding-block: 8px !important;
	font-size: 14px !important;
	text-align: left !important;
	cursor: pointer;
}

.option-item:hover {
	background-color: #cccccc4b;
}

.marked-as-resolved {
	display: none;
}
</style>

<style>
.thread-card-header-left .velt-user-avatar {
	height: 18px !important;
	width: 18px !important;
}


app-comment-dialog-thread-card-reaction-tool {
	display: flex;
	align-items: center;
	justify-content: center;
}

velt-reaction-tool-wireframe {
	display: flex;
	cursor: pointer;
}

.velt-comment-dialog {
	border-radius: 4px !important;
	border: 1px solid #ccc;
}

.velt-comment-dialog[data-velt-comment-dialog-comments-status="RESOLVED"] {
	.marked-as-resolved {
		display: flex;
	}
}

.velt-comment-dialog.velt-comment-dialog--no-comments {
	padding: 8px !important;

	.first-message {
		display: flex;
	}
}

.velt-comment-dialog.velt-comment-dialog--bottom-sheet {
	border-bottom-left-radius: 0 !important;
	border-bottom-right-radius: 0 !important;
}

.velt-comment-dialog .dropdown-container .v-dropdown-menu-trigger {
	padding: 4px 6px 4px 8px;
}

.velt-thread-card--message {
	padding-left: 28px !important;
}

.velt-thread-card--time {
	font-size: 12.5px !important;
	opacity: 0.7 !important;
}

.velt-composer-input--message {
	font-size: 12px !important;
}

.velt-thread-card--reactions {
	padding-left: 28px !important
}

.velt-thread-card--reactions .velt-reaction-pin--default {
	border: 0px !important;
	gap: 4px !important;
}

.velt-thread-card--reactions .velt-reaction-pin--default.active {
	background-color: #cccccc4b !important;
}

.velt-thread-card--reactions .velt-reaction-pin--default .velt-reaction-pin--emoji {
	svg {
		width: 16px !important;
		height: 16px !important;
	}

	image {
		width: 16px !important;
		height: 16px !important;
	}
}

.velt-reaction-pin .velt-reaction-pin--count {
	font-size: 13px !important;
	line-height: 13px !important;
}

.thread-card-header-avatar-container {
	snippyly-user-avatar {
		display: flex !important;
	}
}

#resolveButton {
	width: 100% !important;
	display: block !important;

	app-comment-dialog-resolve-button app-resolve-button {
		button.__button {
			--velt-border-color: transparent !important;
			margin: 0 !important;
			padding: 0 !important;
			width: 100% !important;
			height: unset !important;
			display: block !important;
		}

		.s-tooltiptext {
			display: none !important;
		}
	}
}

.snippyly-menu .mat-mdc-menu-content {
	border-radius: 4px !important;
	border: 1px solid #ccc;
}

.velt-comment-bubble[data-velt-comment-bubble-comments-count="0"] {
	app-comment-bubble-comments-count {
		display: none;
	}
}

velt-comment-tool {
	&:empty {
		display: none;
	}
}
</style>
