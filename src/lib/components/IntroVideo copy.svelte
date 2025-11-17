<script>
    import { onMount } from "svelte";

    let showIntro = true;
    let fadeOut = false;
    let videoElement;
    let isVideoLoaded = false;
    let isVideoReady = false;

    onMount(() => {
        document.body.style.overflow = "hidden";

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

        // ✅ 7 seconds बाद intro remove
        setTimeout(() => {
            fadeOut = true;
            setTimeout(() => {
                showIntro = false;
                document.body.style.overflow = ""; // restore scroll
            }, 800); // fadeOut delay
        }, 7000);
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
            document.body.style.overflow = "";
        }, 800);
    }
</script>

{#if showIntro}
    <div class="intro-container" class:fade-out={fadeOut}>
        {#if !isVideoReady || !isVideoLoaded}
            <div class="loading-overlay">
                <div class="loading-spinner">
                    <div class="spinner"></div>
                    <p>Loading video...</p>
                </div>
            </div>
        {/if}
        
        <video
            bind:this={videoElement}
            src="/videos/Archideus Landing Intro.mp4"
            muted
            playsinline
            preload="auto"
            on:ended={handleVideoEnd}
            class="intro-video"
            class:video-hidden={!isVideoReady || !isVideoLoaded}
        >
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

    .loading-overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #000;
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 10001;
    }

    .loading-spinner {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        color: white;
    }

    .spinner {
        width: 50px;
        height: 50px;
        border: 3px solid rgba(255, 255, 255, 0.2);
        border-radius: 50%;
        border-top-color: white;
        animation: spin 1s ease-in-out infinite;
        margin-bottom: 20px;
    }

    @keyframes spin {
        to { transform: rotate(360deg); }
    }

    .loading-spinner p {
        font-size: 16px;
        margin: 0;
        font-weight: 300;
        opacity: 0.8;
    }

    .skip-button {
        position: absolute;
        top: 30px;
        right: 30px;
        background: rgba(255, 255, 255, 0.2);
        border: 2px solid rgba(255, 255, 255, 0.3);
        color: white;
        padding: 12px 24px;
        border-radius: 30px;
        cursor: pointer;
        font-size: 16px;
        font-weight: 500;
        backdrop-filter: blur(10px);
        transition: all 0.3s ease;
        z-index: 10002;
        opacity: 0;
        pointer-events: none;
    }

    .skip-button.button-visible {
        opacity: 1;
        pointer-events: auto;
    }

    .skip-button:hover {
        background: rgba(255, 255, 255, 0.3);
        border-color: rgba(255, 255, 255, 0.5);
        transform: translateY(-2px);
    }

    .skip-button:active {
        transform: translateY(0);
    }

    /* Mobile responsiveness */
    @media (max-width: 768px) {
        .skip-button {
            top: 20px;
            right: 20px;
            padding: 10px 20px;
            font-size: 14px;
        }

        .spinner {
            width: 40px;
            height: 40px;
        }

        .loading-spinner p {
            font-size: 14px;
        }
    }

    /* Global styles to hide scrollbars during intro */
    :global(body) {
        scrollbar-width: none; /* Firefox */
        -ms-overflow-style: none; /* IE and Edge */
    }

    :global(body::-webkit-scrollbar) {
        display: none; /* Chrome, Safari and Opera */
    }
</style>
