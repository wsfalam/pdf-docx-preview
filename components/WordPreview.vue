<template>
	<div>
		<h2>Previewing DOCX File: {{ fileName }}</h2>
		<div class="" v-if="docxContent" v-html="docxContent"></div>
	</div>
</template>

<script setup>
	import { ref, onMounted } from "vue";
	import mammoth from "mammoth";

	const docxContent = ref("");
	const fileName = ref("");

	onMounted(async () => {
		const filePath = "/sample_doc.docx"; // Replace with your local file path
		try {
			const response = await fetch(filePath);
			const arrayBuffer = await response.arrayBuffer();
			const result = await mammoth.convertToHtml({ arrayBuffer });
			docxContent.value = result.value; // The generated HTML
			fileName.value = filePath.split("/").pop(); // Get the file name from path
		} catch (error) {
			console.error("Error loading .docx file:", error);
		}
	});
</script>

<style scoped>
	/* Add any styles you need here */
</style>
