<script>
	import favicon from "$lib/assets/favicon.svg";
	import Footer from "$lib/components/footer.svelte";
	import Navbar from "$lib/components/Navbar.svelte";
	import OtherNavbar from "$lib/components/OtherNavbar.svelte";
	import "../app.css";
	import { page } from "$app/stores";
	import { afterNavigate } from "$app/navigation";
	import { onMount, tick } from "svelte";
	import { gsap } from "gsap";
	import { ScrollTrigger } from "gsap/ScrollTrigger";
	import { ScrollSmoother } from "gsap/ScrollSmoother";

	gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

	let smoother;

	onMount(() => {
		smoother = ScrollSmoother.create({
			wrapper: "#smooth-wrapper",
			content: "#smooth-content",
			smooth: 1.5,
			effects: true,
			smoothTouch: 0.1
		});

		return () => {
			if (smoother) smoother.kill();
		};
	});

	afterNavigate(async () => {
		await tick();
		
		// Try multiple methods to ensure scroll to top
		window.scrollTo(0, 0);
		document.documentElement.scrollTop = 0;
		document.body.scrollTop = 0;
		
		// Also scroll the smooth wrapper
		const wrapper = document.getElementById('smooth-wrapper');
		if (wrapper) {
			wrapper.scrollTop = 0;
		}
		
		// Use ScrollSmoother if available
		setTimeout(() => {
			if (smoother) {
				smoother.scrollTo(0, false);
			}
		}, 10);
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<!-- ✅ Navbar OUTSIDE smooth scroll wrapper so it stays fixed -->
{#if $page.url.pathname === "/"}
	<Navbar />
{:else}
	<OtherNavbar />
{/if}

<div id="smooth-wrapper">
	<div id="smooth-content">
		<div class="main">
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
