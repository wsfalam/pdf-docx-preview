<template>
	<div>
		<iframe
			ref="csvIframe"
			style="width: 100%; height: 400px"
			frameborder="0"></iframe>
	</div>
</template>

<script setup>
	import Papa from "papaparse";

	const csvIframe = ref(null);

	const fetchCSV = async () => {
		try {
			const response = await fetch("/addresses.csv");
			const data = await response.text();
			parseCSV(data);
		} catch (error) {
			console.error("Error fetching CSV file:", error);
		}
	};

	const parseCSV = (data) => {
		Papa.parse(data, {
			complete: (results) => {
				displayCSV(results.data);
			},
			header: false,
		});
	};

	const displayCSV = (rows) => {
		let tableHtml =
			'<table id="csvTable" style="width: 100%; border-collapse: collapse;">';

		rows.forEach((row) => {
			tableHtml += "<tr>";
			row.forEach((col) => {
				tableHtml += `<td style="border: 1px solid black; padding: 8px; text-align: left;">${col.trim()}</td>`;
			});
			tableHtml += "</tr>";
		});

		tableHtml += "</table>";
		const iframeDoc =
			csvIframe.value.contentDocument || csvIframe.value.contentWindow.document;
		iframeDoc.open();
		iframeDoc.write("<html><body>" + tableHtml + "</body></html>");
		iframeDoc.close();
	};

	onMounted(() => {
		fetchCSV();
	});
</script>
