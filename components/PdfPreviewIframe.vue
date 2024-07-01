<template>
	<div class="max-w-screen-md mx-auto">
		<iframe
			width="700"
			height="500"
			allowfullscreen
			:src="pdfUrl"
			frameborder="0"
			scrolling="auto"></iframe>
	</div>
</template>

<script setup>
	const pdfUrl = "/sample_pdf.pdf";
</script>
