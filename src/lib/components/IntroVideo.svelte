<script>
    import { onMount, onDestroy } from "svelte";

    let showIntro = true;
    let fadeOut = false;
    let videoElement;
    let isVideoLoaded = false;
    let isVideoReady = false;

    let preventScroll;

    onMount(() => {
        if (typeof window !== "undefined" && typeof document !== "undefined") {
            document.body.style.overflow = "hidden";
            window.scrollTo(0, 0);

            preventScroll = (e) => {
                e.preventDefault();
                e.stopPropagation();
                window.scrollTo(0, 0);
                return false;
            };

            window.addEventListener("wheel", preventScroll, { passive: false });
            window.addEventListener("touchmove", preventScroll, {
                passive: false,
            });
            window.addEventListener("scroll", preventScroll, {
                passive: false,
            });
        }

        if (videoElement) {
            videoElement.addEventListener("loadeddata", () => {
                isVideoLoaded = true;
                checkVideoReady();
            });

            videoElement.addEventListener("canplaythrough", () => {
                isVideoReady = true;
                checkVideoReady();
            });

            videoElement.load();
        }

        setTimeout(() => {
            fadeOut = true;
            setTimeout(() => {
                showIntro = false;
                cleanupScrollLock();
            }, 800);
        }, 8000);
    });

    function cleanupScrollLock() {
        if (typeof window !== "undefined" && typeof document !== "undefined") {
            document.body.style.overflow = "";
            window.removeEventListener("wheel", preventScroll);
            window.removeEventListener("touchmove", preventScroll);
            window.removeEventListener("scroll", preventScroll);
        }
    }

    onDestroy(() => {
        cleanupScrollLock();
    });

    function checkVideoReady() {
        if (isVideoLoaded && isVideoReady && videoElement) {
            setTimeout(() => {
                videoElement.play().catch((err) => {
                    console.log("Autoplay prevented:", err);
                });
            }, 100);
        }
    }

    function handleVideoEnd() {
        fadeOut = true;
        setTimeout(() => {
            showIntro = false;
            cleanupScrollLock();
        }, 800);
    }
</script>

{#if showIntro}
    <div class="intro-container" class:fade-out={fadeOut}>
        <video
            bind:this={videoElement}
            muted
            playsinline
            preload="auto"
            on:ended={handleVideoEnd}
            class="intro-video"
            class:video-hidden={!isVideoReady || !isVideoLoaded}
        >
            <source
                src="/videos/Archideus Loader vertical.mp4"
                type="video/mp4"
                media="(max-width: 768px)"
            />
            <source src="/videos/Archideus Loader .mp4" type="video/mp4" />
            Your browser does not support the video tag.
        </video>
    </div>
{/if}

<style>
    .intro-container {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background: #000;
        z-index: 9999;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
        opacity: 1;
        transition: opacity 0.8s ease-out;
    }

    .intro-container.fade-out {
        opacity: 0;
    }

    .intro-video {
        width: 100%;
        height: 100%;
        object-fit: cover;
        opacity: 1;
        transition: opacity 0.5s ease-in;
    }

    .intro-video.video-hidden {
        opacity: 0;
    }
</style>
