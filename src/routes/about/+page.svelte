<script>
    import { onMount, onDestroy } from "svelte";
    import { browser } from "$app/environment";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/dist/ScrollTrigger";
    import AboutTxtHero from "$lib/components/AboutTxtHero.svelte";

    let containerRef;
    let heroTextRef;

    onMount(() => {
        if (!browser) return;

        // Register ScrollTrigger plugin
        gsap.registerPlugin(ScrollTrigger);

        // Split text function
        const splitText = (selector) => {
            const elem = document.querySelector(selector);
            if (!elem) return [];

            const text = elem.innerText;
            const chars = text.split("");
            const charsContainer = document.createElement("div");
            const charsArray = [];

            charsContainer.style.position = "relative";
            charsContainer.style.display = "inline-block";

            chars.forEach((char) => {
                const charContainer = document.createElement("div");

                charContainer.style.position = "relative";
                charContainer.style.display = "inline-block";
                charContainer.innerText = char === " " ? "\u00A0" : char; // Use non-breaking space for spaces
                charsContainer.appendChild(charContainer);

                charsArray.push(charContainer);
            });

            // Remove current text
            elem.innerHTML = "";
            // Append new structure
            elem.appendChild(charsContainer);

            return charsArray;
        };

        // Animate function with infinite loop
        const animate = function () {
            const chars = splitText(".hero p");

            // Create timeline for infinite animation
            const tl = gsap.timeline({ repeat: -1, repeatDelay: 2 });

            // Initial animation - characters slide up from below
            tl.fromTo(
                chars,
                {
                    y: 100,
                    opacity: 0,
                },
                {
                    duration: 0.2,
                    y: 0,
                    opacity: 1,
                    stagger: 0.1,
                    delay: 1,
                    ease: "power2.out",
                },
            )
                // Hold the text visible for a moment
                .to({}, { duration: 1.5 })
                // Fade out animation
                .to(chars, {
                    duration: 0.15,
                    y: -50,
                    opacity: 0,
                    stagger: 0.05,
                    ease: "power2.in",
                });

            return tl;
        };

        // Call the animation
        animate();

        const sections = gsap.utils.toArray(".section");

        sections.forEach((section, index) => {
            ScrollTrigger.create({
                trigger: section,
                start: "top top",
                end: () =>
                    `+=${window.innerHeight * (sections.length - index)}`,
                pin: true,
                pinSpacing: false,
                // markers: false, // Set to true for debugging
            });
        });

        // Cleanup function
        return () => {
            ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
        };
    });

    onDestroy(() => {
        if (browser) {
            ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
        }
    });
</script>

<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700&family=Instrument+Sans:wght@400;500;600;700&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div class="container">
    <AboutTxtHero />

    <div class="container-1" bind:this={containerRef}>
        <div class="section section-1">
            <p>
                Archideus is a full-spectrum architectural practice led by the
                demands of function, not trends.
            </p>
            <img
                src="/man-walking-behind-glass-doors-2025-10-17-01-24-17-utc 1.png"
                alt="Section 1 Image"
            />
        </div>

        <div class="section section-2">
            <p>
                Every project begins with clarity,
                <br />
                <span class="it">
                    What the space is meant to do,
                    <br />
                    Who it must serve,
                    <br />
                    How it should endure.
                </span>
            </p>
            <img src="/final copy1 2.png" alt="Section 2 Image" />
        </div>

        <div class="section section-3">
            <p>
                From site planning to the last fixture, we <br />
                shape environments that earn their place:
                <br />
                <span class="it">
                    practical, precise, and purposeful by design.
                </span>
            </p>
            <video class="section-3-video" autoplay muted loop playsinline>
                <source src="/Untitled design.mp4" type="video/mp4" />
                Your browser does not support the video tag.
            </video>
        </div>

        <div class="section section-4">
            <div class="section-4-descr">
                <h4>Shaping Archideus</h4>
                <div class="text-block">
                    <span>
                        Meet Vaasudev, the founder of Archideus. He is the heart
                        and spirit behind the practice, driven by the belief
                        that architecture is not only about structures but about
                        the emotions a space can hold.<br />
                        <div class="hieght"></div>
                        For him, what matters most is making it possible—doing whatever
                        it takes to shape a space into what it is meant to be.
                    </span>
                    <!-- <div class="hieght"></div> -->
                    <span>
                        <span class="desc-special">
                            Vasu's process always begins on paper, sketching by
                            hand to translate emotions into lines.
                        </span>
                        <div class="hieght"></div>
                        These blueprints are more than technical drawings; they are
                        the first step in turning intention into form, guiding spaces
                        that are functional, enduring, and deeply human.
                    </span>
                </div>
            </div>
            <div class="image-section-4">
                <div class="frame">
                    <img
                        src="/Group 35.png"
                        alt="Happy couple at home"
                        class="sec-image"
                    />
                </div>
                <div class="sec-4-img-txt">
                    <h3 class="sec-4-head">Ar. Vaasudev Samrat,</h3>
                    <div class="sec-4-des">
                        Studio head Architect, Concept Design Head
                    </div>
                </div>
            </div>

            <!-- <img src="/aboutus2.png" alt="Section 4 Image" /> -->
        </div>
    </div>

    <div class="content-2">
        <h3>The Archideus Journal</h3>
        <div class="content-2-description">
            <p>
                Dive into our thoughts, process, and inspirations. From design
                insights to behind-the-scenes stories — explore how we think,
                build, and imagine at Archideus
            </p>
            <button> Read Our stories </button>
        </div>
    </div>

    <div class=" content-3">
        <div class="content-3-tab">
            <a href="/blog">
                <div class=" content-3-card">
                    <div class=" content-3-card-image">
                        <img
                            src="/arrow.png"
                            alt="Image 3"
                            class="content-3-image2"
                        />
                        <img
                            src="/image 83.png"
                            alt="Image 3"
                            class="content-3-image1"
                        />
                    </div>
                    <div class=" content-3-card-header">
                        <div class=" content-3-card-description">
                            <p>
                                The Science Behind Timeless Materials: Why
                                Concrete, Steel, and Wood Still Reign in Modern
                                Architecture
                            </p>
                        </div>
                        <!-- <h4>
                            The Science Behind Timeless Materials: Why Concrete,
                            Steel, and Wood Still Reign in Modern Architecture
                        </h4> -->
                        <div>
                            <span> 12min </span>
                        </div>
                    </div>
                </div>
            </a>
            <a href="/blog/2">
                <div class=" content-3-card">
                    <div class=" content-3-card-image">
                        <img
                            src="/arrow.png"
                            alt="Image 3"
                            class="content-3-image2"
                        />
                        <img
                            src="/background-with-the-texture-of-an-old-stump-2025-03-14-00-23-11-utc 1.png"
                            alt="Image 3"
                            class="content-3-image1"
                        />
                    </div>
                    <div class=" content-3-card-header">
                        <div class=" content-3-card-description">
                            <p>
                                The Craft of Matter: How Material Choice Tells a
                                Story in Architecture
                            </p>
                        </div>
                        <span> 15min </span>
                    </div>
                </div>
            </a>
        </div>
        <a href="/blog/1">
            <div class=" content-3-card">
                <div class=" content-3-card-image">
                    <img
                        src="/arrow.png"
                        alt="Image 3"
                        class="content-3-image2"
                    />
                    <img
                        src="/blog21.png"
                        alt="Image 3"
                        class="content-3-image1"
                    />
                </div>
                <div class=" content-3-card-header">
                    <div class=" content-3-card-description">
                        <p>
                            Biophilic Design: Where Neuroscience Meets
                            Architecture
                        </p>
                    </div>
                    <span> 10min </span>
                </div>
            </div>
        </a>
    </div>

    <div class="content-4">
        <h3>
            <span>If you've come this far,</span>
            <span>Then you're already imagining it.</span>
            <span class="itallic">Lets bring it to life.</span>
        </h3>
        <button>Just Say Hello</button>
    </div>
</div>

<style>
    @import url("./index.css");

    .hoverme {
        transition: all 0.7s ease;
    }
    .hieght {
        height: 14px !important;
        /* background-color: aqua !important; */
        width: 100% !important;
    }
    .desc-special {
        margin-top: 0% !important;
        /* background-color: aqua; */
        color: #000;
        font-family: "Instrument Sans";
        font-size: 24px;
        font-style: italic !important;
        font-weight: 500;
        /* line-height: 36px; */
    }
    .image-section-4 {
        position: relative;

        /* background-color: aqua; */
        width: 40%;
        padding-top: 5vmax;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    }
    .sec-image {
        position: relative;
    }

    .frame img {
        width: 533px;
        height: 533px;
        flex-shrink: 0;
        aspect-ratio: 1/1;
    }
    .hoverme:hover {
        scale: 1.1;
        text-decoration: none;
    }
    .sec-4-img-txt {
        position: absolute;
        bottom: 0;
        padding: 0%;
        left: 2vmax;
        height: 23%;
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: start;
        gap: 0;
        /* padding-left: 2vmax; */
        /* background-color: #8c3d3d; */
    }
    .sec-4-head {
        /* background-color: aqua; */
        margin-bottom: 2vmax;
    }

    :root {
        --primary-color: #8c3d3d;
        --text-color: #333;
        --max-width: 1300px;
    }
    .sec-4-des {
        margin: 0% !important;
        padding: 0% !important;
        /* background-color: aqua; */
        color: #8c3d3d !important;
        font-family: "Instrument Sans" !important;
        font-size: 16px !important;
        font-style: normal !important;
        font-weight: 600 !important;
        line-height: 0px !important;
    }
    /* Responsive */
    @media (max-width: 1024px) {
        .container {
            gap: 30px;
            padding: 40px 30px;
        }

        .blank-section {
            display: none; /* hide spacing column on tablets */
        }
    }
    /* 📱 Mobile (up to 768px) - Content 3 & 4 */
    @media (max-width: 768px) {
        /* Content 3 Styles */
        .content-3 {
            flex-direction: column !important;
            width: 95% !important;
            gap: 4vmax !important;
            padding-top: 8vmax !important;
        }

        .content-3-tab {
            flex-direction: column !important;
            width: 100% !important;
            gap: 4vmax !important;
        }

        .content-3-card {
            width: 100% !important;
            min-width: auto !important;
            max-width: 100% !important;
            height: auto !important;
        }

        .content-3-image1 {
            height: 220px !important;
        }

        /* Content 4 Styles */
        .content-4 {
            width: 95% !important;
            gap: 3vmax !important;
            margin-top: 8vmax !important;
            align-items: center !important;
        }

        .content-4 h3 {
            font-size: 32px !important;
            line-height: 40px !important;
            text-align: center !important;
            width: 100% !important;
        }

        .content-4 h3 span {
            display: block !important;
        }

        .content-4 button {
            width: 100% !important;
            max-width: 280px !important;
            font-size: 18px !important;
        }

        /* Image Section 4 Mobile Adjustments */
        .image-section-4 {
            width: 100% !important;
            padding-top: 0 !important;
            height: auto !important;
            display: flex !important;
            flex-direction: column !important;
            justify-content: center !important;
            align-items: center !important;
            gap: 2rem !important;
        }

        .frame {
            width: 100% !important;
            display: flex !important;
            justify-content: center !important;
            align-items: center !important;
        }

        .frame img {
            width: 100% !important;
            height: auto !important;
            max-width: 400px !important;
        }

        .sec-4-img-txt {
            position: static !important;
            display: flex !important;
            flex-direction: column !important;
            justify-content: center !important;
            align-items: center !important;
            width: 100% !important;
            padding: 0 1rem !important;
            gap: 0.5rem !important;
            height: auto !important;
        }

        .sec-4-head {
            font-size: 24px !important;
            text-align: center !important;
            margin-bottom: 0 !important;
            white-space: normal !important;
            line-height: 1.3 !important;
        }

        .sec-4-des {
            font-size: 14px !important;
            text-align: center !important;
            white-space: normal !important;
            line-height: 1.4 !important;
            word-wrap: break-word !important;
            margin: 0 !important;
            padding: 0 !important;
        }
    }

    @media (max-width: 768px) {
        .container {
            flex-direction: column;
            text-align: center;
            gap: 30px;
            padding: 40px 20px;
        }

        .blank-section {
            display: none; /* no blank space on mobile */
        }

        .circle {
            display: none; /* remove circle for simplicity */
        }

        .text-section p {
            margin: 0 auto;
        }
    }

    @media (max-width: 768px) {
        .container {
            flex-direction: column;
            text-align: center;
            gap: 30px;
            padding: 40px 20px;
        }

        .text-section,
        .image-section {
            flex: 1 1 100%;
        }

        .image-section {
            order: -1; /* move image above text */
        }

        .blank-section {
            display: none; /* no blank space on mobile */
        }

        .circle {
            display: none; /* remove circle for simplicity */
        }

        .text-section p {
            margin: 0 auto;
        }
        .frame img {
            width: 40vmax !important;
            height: 533px;
            flex-shrink: 0;
            aspect-ratio: 1/1;
        }
    }

    /* 📱 Very Small Mobile (up to 480px) - Additional adjustments */

    /* Content 2 Responsive (if needed) */
</style>
