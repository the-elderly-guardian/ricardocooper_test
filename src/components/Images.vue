<script setup>
import ImagePopup from './ImagePopup.vue'

import axios from 'axios'
import { ref } from 'vue'

let isImagesLoaded = ref(false)
let isShowPopup = ref(false)

let targetImageId = ref(-1)

let images = ref([])

function loadImages() {
	axios.get("https://boiling-refuge-66454.herokuapp.com/images")
	.then(response => {
		isImagesLoaded.value = true
		images.value = response.data
	})
	.catch(error => {
		alert(error)
	})
}

function loadImagePopup(card) {
	targetImageId.value = card.target.id
	isShowPopup.value = true
}

loadImages()
</script>

<template>
	<ImagePopup v-bind:imageId="targetImageId" v-if="isShowPopup" @close="isShowPopup = false"/>
	
	<div class="images" v-if="isImagesLoaded">
		<div v-for="image in images" class="image-card" @click="loadImagePopup">
			<img v-bind:id="image.id" v-bind:src="image.url"/>
			<span>id: {{image.id}}</span>
		</div>
	</div>
</template>

<style scoped>
.images {
	min-width: calc(100% - 64px);
	max-width: calc(100% - 64px);
	
	margin-top: 32px;
	margin-left: 32px;
	margin-right: 32px;

	display: flex;
	
	flex-direction: row;
	flex-wrap: wrap;
	
	justify-content: center;
}

.image-card {
	margin: 32px;
	
	display: flex;
	
	flex-direction: column;
	
	cursor: pointer;
}

.image-card > img {
	min-width: 300px;
	max-width: 300px;
	min-height: 200px;
	max-height: 200px;
	
	margin-bottom: 8px;
	
	border-radius: 8px;
	
	background-size: contain;
}

.image-card > span {
	font-style: normal;
	font-weight: 500;
	font-size: 14px;
	line-height: 20px;
}
</style>
