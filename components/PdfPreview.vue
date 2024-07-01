<template>
	<div>
		<div class="my-6">
			<VuePdf
				class="max-w-screen-md mx-auto border my-2"
				v-for="page in numOfPages"
				:key="page"
				:src="pdfSrc"
				:page="page" />
		</div>
	</div>
</template>

<script setup>
	const pdfSrc = ref("/sample_pdf.pdf");
	const numOfPages = ref(0);

	let VuePdf, createLoadingTask;

	import("vue3-pdfjs/esm")
		.then((module) => {
			VuePdf = module.VuePdf;
			createLoadingTask = module.createLoadingTask;

			// Load the PDF
			const loadingTask = createLoadingTask(pdfSrc.value);
			loadingTask.promise.then((pdf) => {
				numOfPages.value = pdf.numPages;
			});
		})
		.catch((err) => console.log(err));

	onMounted(() => {
		// Any other client-only code can go here
	});
</script>
