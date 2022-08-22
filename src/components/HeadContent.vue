<script setup>
</script>

<template>
	<div class="head-content">
		<div>
			<div>
				<div class="head-content-user-avatar">
				</div>
				
				<span class="head-content-user-name">Ricardo Cooper</span>
			</div>
			<div>
				<a class="head-content-button" href="#">
					<i class="material-icons">mail</i>
					Message
				</a>
				<a class="head-content-button" href="#">
					<i class="material-icons">call</i>
					Call
				</a>
			</div>
		</div>
	</div>
</template>

<style scoped>
.head-content {
	min-width: calc(100% - 64px);
	max-width: calc(100% - 64px);
	min-height: 192px;
	max-height: 192px;
	
	margin-bottom: 110px;
	
	margin-top: 32px;
	margin-left: 32px;
	margin-right: 32px;
	
	display: flex;
	
	justify-content: center;
	
	background-image: url(/banner.png);
	background-repeat: no-repeat;
	background-size: cover;
}

.head-content > div,
.head-content > div > div {
	display: inline-flex;
	align-items: flex-end;
}

.head-content > div {
	min-width: 65%;

	position: absolute;
	
	margin-top: 128px;
	
	justify-content: space-between;
}

.head-content-user-avatar {
	min-width: 128px;
	max-width: 128px;
	min-height: 128px;
	max-height: 128px;

	background-image: url(/avatar.png);
	background-repeat: no-repeat;
	background-size: contain;
}

.head-content-user-name {
	margin-left: 20px;

	font-style: normal;
	font-weight: 700;
	font-size: 24px;
	line-height: 32px;
}

.head-content-button {
	box-sizing: border-box;

	font-weight: 500;
	font-size: 14px;
	line-height: 20px;
	
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	padding: 9px 17px 9px 13px;
	gap: 8px;
	
	background: #FFFFFF;

	border: 1px solid #D1D5DB;

	box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
	border-radius: 6px;
	
	border-radius: 6px;
	
	text-align: center;
	
	flex: none;
	order: 0;
	flex-grow: 0;
}

.head-content-button:not(:last-child) {
	margin-right: 16px;
}

@media screen and (max-width: 860px) {
	.head-content {
		margin-bottom: 160px;
	}
	
	.head-content > div,
	.head-content > div > div {
		display: flex;
		flex-direction: column;
	}
	
	.head-content > div {
		justify-content: center;
		align-items: center;
	}
	
	.head-content > div > div:not(:last-child) {
		justify-content: center;
		align-items: center;
	}
	
	.head-content > div > div:not(:first-child) {
		flex-direction: row;
	}
	
	.head-content-user-name {
		margin-left: unset;
	}
}
</style>
