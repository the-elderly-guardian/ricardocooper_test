<script setup>
import { ref, watch } from 'vue'
import axios from 'axios'

const props = defineProps(['imageId'])

const userName = ref(null)
const commentText = ref(null)

let previewImageLink = ref("")
let commentaries = ref([])

function sendComment() {
	axios.post("https://boiling-refuge-66454.herokuapp.com/images/" + props.imageId + "/comments", {
		name: userName.value.value,
		comment: commentText.value.value
	})
	.then(response => {
		userName.value.value = ""
		commentText.value.value = ""
	})
	.catch(error => {
		alert(error)
	})
}

function proceedCommentaries() {
	for(const comment of commentaries.value) {
		comment.date = new Date(comment.date).toLocaleTimeString("en-US")
	}
}

axios.get("https://boiling-refuge-66454.herokuapp.com/images/" + props.imageId)
.then(response => {
	previewImageLink.value = response.data.url
	commentaries.value = response.data.comments
	
	proceedCommentaries()
})
.catch(error => {
	alert(error)
})
</script>

<template>
	<div class="image-popup">
		<div class="image-popup-window-background" @click="$emit('close')">
		</div>
		<div class="image-popup-window">
			<img v-bind:src="previewImageLink"/>
			<div>
				<label for="image-popup-window-user-name">Name</label>
				<input ref="userName" type="text" id="image-popup-window-user-name"/>
				
				<label for="image-popup-window-user-comment">Comment</label>
				<textarea ref="commentText" id="image-popup-window-user-comment" rows="5"></textarea>
				<span class="sub-text">Write a few sentences about the photo.</span>
			</div>
			<a href="#" @click="sendComment">Save</a>
			<div v-if="commentaries.length > 0">
				<span>Comments</span>
				<ul>
					<li v-for="comment in commentaries">
						<span>{{comment.text}}</span>
						<span>{{comment.date}}</span>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<style scoped>
.image-popup {
	min-width: 100vw;
	max-width: 100vw;
	min-height: 100vh;
	max-height: 100vh;
	
	top: 0px;
	left: 0px;
	
	position: fixed;
	
	display: flex;
	
	justify-content: center;
	align-items: center;
	
	z-index: 100;
}

.image-popup-window-background {
	min-width: 100vw;
	max-width: 100vw;
	min-height: 100vh;
	max-height: 100vh;
	
	top: 0px;
	left: 0px;

	z-index: 101;

	position: fixed;
	
	background: rgba(107, 114, 128, 0.75);
}

.image-popup-window {
	max-width: 60%;
	max-height: 80%;

	position: fixed;
	
	padding: 24px;
	gap: 24px;
	
	align-items: center;
	
	background-color: #ffffff;
	
	box-shadow: 0px 20px 25px -5px rgba(0, 0, 0, 0.1), 0px 10px 10px -5px rgba(0, 0, 0, 0.04);
border-radius: 8px;

	overflow-y: scroll;
	overflow-x: hidden;

	z-index: 102;
}

.image-popup-window,
.image-popup-window > div {
	display: flex;
	flex-direction: column;
}

.image-popup-window > img {
	min-width: 400px;
	max-width: 400px;
	min-height: 300px;
	max-height: 300px;
	
	margin-left: 143px;
	margin-right: 143px;
	
	box-shadow: 0px 25px 50px -12px rgba(0, 0, 0, 0.25);
	border-radius: 24px;
}

.image-popup-window > div {
	min-width: 100%;
	max-width: 100%;
}

.image-popup-window > div > textarea,
.image-popup-window > div > input {
	marign-top: 4px;
	margin-bottom: 8px;

	background: #FFFFFF;

	border: 1px solid #D1D5DB;

	box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
	border-radius: 6px;
	
	resize: none;
}

.sub-text {
	font-style: normal;
	font-weight: 400;
	font-size: 14px;
	line-height: 20px;
	
	color: #6B7280;
}

.image-popup-window > a {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	padding: 9px 17px;
	
	color: #FFFFFF;
	background: #4F46E5;

	box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
	border-radius: 6px;
}

.image-popup-window > div > ul > li {
	display: flex;
	
	flex-direction: column;
	
	font-size: 12px;
}
</style>

<script>
export default {
	activated() {
		console.log("activ");
	},
	deactivated() {
		console.log("deactiv");
	}
}
</script>
