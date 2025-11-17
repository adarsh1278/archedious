<script>
	import favicon from "$lib/assets/favicon.svg";
	import Footer from "$lib/components/footer.svelte";
	import Navbar from "$lib/components/Navbar.svelte";
	import OtherNavbar from "$lib/components/OtherNavbar.svelte"; // agar dusre pages ke liye dusri navbar chahiye
	import "../app.css";

	import { page } from "$app/stores";
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="main">
	<!-- ✅ Conditional Navbar -->
	{#if $page.url.pathname === "/"}
		<Navbar />
	{:else}
		<OtherNavbar />
	{/if}

	<!-- ✅ Page Content -->
	<slot />

	<Footer />
</div>

<style>
	.main {
		/* min-height: 100dvh; */
		display: grid;
		grid-template-rows: auto 1fr auto;
	}
</style>
