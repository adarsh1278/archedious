<script>
    import { onMount } from "svelte";

    onMount(() => {
        const timer = setTimeout(() => {
            const svg = document.querySelector(".text-mask");
            if (svg) {
                svg.classList.add("fade-out");
            }
        }, 2800); //

        return () => clearTimeout(timer);
    });
</script>

<section class="hero">
    <video autoplay muted loop playsinline class="bg-video">
        <source src="/videos/hero.mp4" type="video/mp4" />
        Your browser does not support the video tag.
    </video>

    <svg
        class="text-mask"
        viewBox="0 0 1000 200"
        preserveAspectRatio="xMidYMid slice"
    >
        <style>
            text {
                font-family: "Playfair Display", sans-serif;
            }

            .txt {
                font-size: 220%;
            }

            .zoom-group {
                transform-origin: 500px 83px; /* Approximate center of "i" */
                animation: zoomIn 5s ease-in-out forwards;
                animation-delay: 1.3s;
            }

            .text-mask.fade-out {
                transition: opacity 0.8s ease;
                opacity: 0;
                pointer-events: none;
            }

            @keyframes zoomIn {
                0% {
                    transform: scale(0.6);
                }
                100% {
                    transform: scale(61);
                    opacity: 1;
                      transform-origin: 500px 83px; /* Approximate center of "i" */
                }
            }
        </style>
        <defs>
            <mask id="text-cutout" x="0" y="0" width="100%" height="100%">
                <rect width="100%" height="100%" fill="white" />
                <g class="zoom-group">
                    <text
                        x="50%"
                        y="50%"
                        class="txt"
                        fill="black"
                        text-anchor="middle"
                        dominant-baseline="middle"
                    >
                        Archideus
                    </text>
                </g>
            </mask>
        </defs>
        <rect width="100%" height="100%" fill="#fff" mask="url(#text-cutout)" />
    </svg>
</section>

<style>
    .text-mask.fade-out {
        transition: opacity 1s ease;
        opacity: 0;
        pointer-events: none;
    }

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

    .text-mask {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 999;
        overflow: hidden;
    }
</style>
