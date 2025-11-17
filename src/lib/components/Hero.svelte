<script>
    import { onMount } from "svelte";

    let heroVideo;

    onMount(() => {
        if (!heroVideo) return;

        // 8.1 seconds बाद video autoplay
        const timer = setTimeout(() => {
            heroVideo.play().catch((err) => {
                console.log("Autoplay prevented:", err);
            });
        },7250);

        return () => clearTimeout(timer);
    });
</script>


<section class="hero">
    
    <video
        bind:this={heroVideo}
        muted
        loop
        preload="auto"
        class="bg-video"
    >
        <source src="/videos/archidues show reel video.mp4" type="video/mp4" />
        Your browser does not support the video tag.
    </video>
</section>

<style>
    .hero {
        position: relative;
        width: 100vw;
        height: 100vh;
        overflow: hidden;
    }

    .bg-video {
        position: absolute;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        object-fit: cover;
    }
</style>
