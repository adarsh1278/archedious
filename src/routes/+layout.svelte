<script>
	import favicon from "$lib/assets/favicon.svg";
	import Footer from "$lib/components/footer.svelte";
	import Navbar from "$lib/components/Navbar.svelte";
	import OtherNavbar from "$lib/components/OtherNavbar.svelte";
	import "../app.css";
	import { page } from "$app/stores";
	import { onMount } from "svelte";
	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/ScrollSmoother";

	gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

	let smoother;

	onMount(() => {
		smoother = ScrollSmoother.create({
			wrapper: "#smooth-wrapper",
			content: "#smooth-content",
			smooth: 1.2,
			effects: true,
			smoothTouch: 0.1,
			normalizeScroll: true
		});

		return () => {
			if (smoother) smoother.kill();
		};
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div id="smooth-wrapper">
	<div id="smooth-content">
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
	</div>
</div>

<style>
	#smooth-wrapper {
		overflow: hidden;
	}

	#smooth-content {
		overflow: visible;
	}

	.main {
		display: grid;
		grid-template-rows: auto 1fr auto;
	}
</style>
