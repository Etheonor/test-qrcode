<script lang="ts">
	import QRCode from '@castlenine/svelte-qrcode';

	let downloadUrlPng = '';

	const handleDownloadUrlGeneratedPng = (url = '') => {
		downloadUrlPng = url;
	};
</script>

<svelte:head>
	<title>Test QRCode component</title>
</svelte:head>

<h1>Standard QR Code</h1>

<h2>With download url generated with responsive</h2>
<div class="test">
	<QRCode
		data="https://duxreserve.com"
		logoPath="/logo/lightning.svg"
		dispatchDownloadUrl
		downloadUrlFileFormat="png"
		isResponsive
		on:downloadUrlGenerated={(event) => {
			console.log(event.detail);
			handleDownloadUrlGeneratedPng(event.detail.url);
		}}
	/>
</div>

{#if downloadUrlPng}
	<a href={downloadUrlPng} download="QR-code-filename" target="_blank">Download QR Code</a>
{/if}

<p>With download url generated for PNG</p>
<div>
	<QRCode
		data="https://duxreserve.com"
		logoPath="/logo/lightning.svg"
		dispatchDownloadUrl
		downloadUrlFileFormat="png"
		on:downloadUrlGenerated={(event) => handleDownloadUrlGeneratedPng(event.detail.url)}
	/>
</div>

{#if downloadUrlPng}
	<a href={downloadUrlPng} download="QR-code-filename-png" target="_blank"
		>Download QR Code in png format</a
	>
{/if}

<style>
	.test {
		max-width: 20%;
	}
</style>
