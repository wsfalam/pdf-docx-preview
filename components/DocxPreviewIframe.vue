<template>
	<div>
		<iframe
			width="100%"
			height="100vh"
			:src="googleDocsUrl"
			frameborder="0"
			scrolling="auto"></iframe>
	</div>
</template>

<script setup>
	import { ref, onMounted } from "vue";

	const googleDocsUrl = ref("");

	onMounted(() => {
		const baseUrl = window.location.origin; // Get the base URL of your app
		const filePath = "sample_doc.docx"; // Path to your .docx file in the public folder
		const docxUrl = `${baseUrl}/${filePath}`;
		googleDocsUrl.value = `https://docs.google.com/viewer?url=${encodeURIComponent(
			docxUrl
		)}&embedded=true`;
	});
</script>

<style scoped>
	/* Additional styles can be applied if needed */
</style>
