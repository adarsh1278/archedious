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
            <img src="/aboutus1.png" alt="Section 1 Image" />
        </div>

        <div class="section section-2">
            <p>
                Every project begins with clarity, what the space is meant to
                do, who it must serve, and how it should endure.
            </p>
            <img src="/hrscroll1.png" alt="Section 2 Image" />
        </div>

        <div class="section section-3">
            <p>
                From site planning to the last fixture, we shape environments
                that earn their place: practical, precise, and purposeful by
                design.
            </p>
            <img src="/hrscroll1.png" alt="Section 3 Image" />
        </div>

        <div class="section section-4">
            <div class="section-4-descr">
                <h4>Shaping Archideus</h4>
                <div class="text-block">
                    <span>
                        Meet Vaasudev, the founder of Archideus. He is the heart
                        and spirit behind the practice, driven by the belief
                        that architecture is not only about structures but about
                        the emotions a space can hold. For him, what matters
                        most is making it possible—doing whatever it takes to
                        shape a space into what it is meant to be.
                    </span>
                    <span>
                        Vasu's process always begins on paper, sketching by hand
                        to translate emotions into lines. These blueprints are
                        more than technical drawings; they are the first step in
                        turning intention into form, guiding spaces that are
                        functional, enduring, and deeply human.
                    </span>
                </div>
            </div>
            <img src="/aboutus2.png" alt="Section 4 Image" />
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
                        <span> 12min </span>
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

    .hoverme:hover {
        scale: 1.1;
        text-decoration: none;
    }
</style>
