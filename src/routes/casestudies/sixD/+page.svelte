<script>
    import { onMount } from "svelte";
    import { page } from "$app/stores";

    let slideIndex = 1;

    onMount(() => {
        // Auto slide functionality
        const autoSlide = () => {
            slideIndex = slideIndex >= 3 ? 1 : slideIndex + 1;
        };

        const interval = setInterval(autoSlide, 5000);

        // Horizontal scroll functionality
        const content1 = document.querySelector(".horizontal-scroll");
        let targetScrollLeft = 0;
        let currentScrollLeft = 0;
        let isAnimating = false;

        if (content1) {
            targetScrollLeft = content1.scrollLeft;
            currentScrollLeft = content1.scrollLeft;

            function smoothScroll() {
                const diff = targetScrollLeft - currentScrollLeft;
                const step = diff * 0.1;

                if (Math.abs(diff) > 0.5) {
                    currentScrollLeft += step;
                    content1.scrollLeft = currentScrollLeft;
                    requestAnimationFrame(smoothScroll);
                } else {
                    currentScrollLeft = targetScrollLeft;
                    content1.scrollLeft = currentScrollLeft;
                    isAnimating = false;
                }
            }

            function isFullyInView(el) {
                const rect = el.getBoundingClientRect();
                return rect.top >= 0 || rect.bottom <= window.innerHeight - 10;
            }

            const handleWheel = (e) => {
                if (e.deltaX) {
                    e.preventDefault();
                    return;
                }
                if (!isFullyInView(content1)) {
                    return;
                }

                if (e.deltaY !== 0) {
                    const atStart = content1.scrollLeft === 0;
                    const atEnd =
                        Math.ceil(content1.scrollLeft + content1.clientWidth) >=
                        content1.scrollWidth;

                    if (
                        !(atStart && e.deltaY < 0) &&
                        !(atEnd && e.deltaY > 0)
                    ) {
                        e.preventDefault();

                        const scrollDistance = e.deltaY * 2;
                        targetScrollLeft = Math.max(
                            0,
                            Math.min(
                                content1.scrollWidth - content1.clientWidth,
                                targetScrollLeft + scrollDistance,
                            ),
                        );

                        if (!isAnimating) {
                            isAnimating = true;
                            currentScrollLeft = content1.scrollLeft;
                            requestAnimationFrame(smoothScroll);
                        }
                    }
                }
            };

            content1.addEventListener("wheel", handleWheel, { passive: false });

            return () => {
                content1.removeEventListener("wheel", handleWheel);
                clearInterval(interval);
            };
        }

        return () => clearInterval(interval);
    });

    function currentSlide(n) {
        slideIndex = n;
    }

    function openVideoLightbox(videoSrc) {
        // Video lightbox functionality
        const videoWrapper = document.getElementById("videoWrapper");
        const modal = document.getElementById("videoLightbox");

        if (videoWrapper && modal) {
            videoWrapper.innerHTML = "";

            const isYouTube = /youtube\.com\/watch\?v=|youtu\.be\//i.test(
                videoSrc,
            );
            const isVimeo = /vimeo\.com\/\d+/i.test(videoSrc);
            const isMp4 =
                /\.mp4(\?|#|$)/i.test(videoSrc) ||
                (/^\/|^https?:/.test(videoSrc) && !isYouTube && !isVimeo);

            let player;

            if (isYouTube) {
                const id = videoSrc.match(/(?:v=|be\/)([^&?]+)/i)?.[1] || "";
                const src = `https://www.youtube.com/embed/${id}?autoplay=1&rel=0&modestbranding=1`;
                player = document.createElement("iframe");
                player.setAttribute("allowfullscreen", "");
                player.setAttribute(
                    "allow",
                    "autoplay; encrypted-media; picture-in-picture",
                );
                player.setAttribute("src", src);
                player.style.border = "0";
            } else if (isVimeo) {
                const id = videoSrc.match(/vimeo\.com\/(\d+)/i)?.[1] || "";
                const src = `https://player.vimeo.com/video/${id}?autoplay=1&title=0&byline=0&portrait=0`;
                player = document.createElement("iframe");
                player.setAttribute("allowfullscreen", "");
                player.setAttribute(
                    "allow",
                    "autoplay; fullscreen; picture-in-picture",
                );
                player.setAttribute("src", src);
                player.style.border = "0";
            } else if (isMp4) {
                player = document.createElement("video");
                player.setAttribute("src", videoSrc);
                player.setAttribute("controls", "");
                player.setAttribute("playsinline", "");
                player.autoplay = true;
                player.style.width = "100%";
                player.style.height = "100%";
            }

            if (player) {
                videoWrapper.appendChild(player);
                // Show modal using Bootstrap if available
                if (typeof bootstrap !== "undefined") {
                    const bsModal = new bootstrap.Modal(modal);
                    bsModal.show();
                }
            }
        }
    }
</script>

<div class="case-study-wrapper">
    <div class="container">
        <div class="hero-bg">
            <div>
                <h1>SixD Office</h1>
                <p>Commercial| Noida</p>
            </div>
        </div>

        <div class="sub-head">
            <h2>A Modern Workspace of Clarity & Confidence</h2>
            <p>
                This workspace balances functional hierarchy with a transparent
                and inclusive environment. From collaborative zones to private
                cabins, every area is structured to encourage clarity and ease
                of interaction. A refined client lounge creates a comfortable
                and inviting experience for all visitors.
            </p>
        </div>

        <!-- <div class="section-2">
            <img src="/Rectangle 159.png" alt="Section 2 Image" />
            <img src="/Rectangle 160.png" alt="Section 2 Image" />
            <img src="/Rectangle 161.png" alt="Section 2 Image" />
        </div> -->

        <!-- <div class="sub-head-2">
            <h2>
                The Starting Point:<br />
                Brand, Behaviour & Bare Bones
            </h2>
        </div> -->

        <div class="horizontal-scroll">
            <!-- <div class="scroll-item-1">
                <img
                    src="/hand sketch 1.png"
                    alt="Image 1"
                    class="scroll-image"
                />
                <p>
                    The first big step was connecting the two floors to create a
                    duplex. This instantly improved how the space functioned. It
                    allowed clear separation between family areas and private
                    rooms, and the staircase became a natural anchor that guided
                    movement and brought in light.
                </p>
            </div>

            <div class="scroll-item-1">
                <img
                    src="/8091bdfa-c3d8-49d8-b6f3-0a039c49705d 1.png"
                    alt="Image 2"
                    class="scroll-image"
                />
                <p>
                    We kept the needs of a multi-generation family at the
                    center. The idea was to create a space where privacy and
                    togetherness both felt natural.
                </p>
            </div>
            <div class="scroll-item-1">
                <img
                    src="/f54ce718-c901-458b-80d4-1be627d98778 1.png"
                    alt="Image 2"
                    class="scroll-image"
                />
                <p>
                    Since the layout was long and narrow, we made every part
                    work harder. We pulled natural light deeper into the space,
                    avoided dead corners, and designed elements to serve more
                    than one purpose. Storage also added warmth, walls supported
                    light flow, and transitions became places to breathe.
                </p>
            </div>
            <div class="scroll-item-2">
                <video class="scroll-video" autoplay muted loop playsinline>
                    <source src="/hrscrollv1.mp4" type="video/mp4" />
                    Your browser does not support the video tag.
                </video>
            </div>

            <div class="scroll-item-3">
                <div class="scroll-item-4">
                    <img
                        src="/FRONT BEDROOM-01 1.png"
                        alt="Image 3"
                        class="scroll-image-3"
                    />
                </div>

                <p>
                    The rooms were designed to adapt as the family grows and
                    changes. Spaces can shift from one purpose to another — from
                    kids to teenagers to elders. The design is flexible enough
                    to evolve with their lives, not hold them back.
                </p>
            </div> -->
            <!-- <div class="scroll-item-5">
                <img src="/Enscape_2024-10-09-16-58-09.jpg" alt="Image 1" />
            </div> -->

            <div class="scroll-item-5">
                <img src="/image 90.png" alt="Image 1" />
            </div>
            <div class="scroll-item-5">
                <img src="/image 91.png" alt="Image 1" />
            </div>
            <div class="scroll-item-5">
                <img src="/image 92.png" alt="Image 1" />
            </div>
        </div>

        <!-- <div class="sub-head">
            <h2>Making Everyday Living Feel Better</h2>
            <p>
                We reimagined the space as something you don’t just see, but
                feel.
            </p>
        </div> -->

        <!-- <div class="hero-2">
            <div class="hero-bg-2">
                <div class="animated-text">
                    <p class="text-1">Living Room</p>
                    <p class="text-2">Master Bedroom</p>
                    <p class="text-3">BathStudio</p>
                </div>
            </div>
        </div> -->

        <!-- <div class="section-3">
            <video class="section-3-video" autoplay muted loop playsinline>
                <source src="/Untitled design.mp4" type="video/mp4" />
                Your browser does not support the video tag.
            </video>

            <div class="section-3-card">
                <h2>Heritage in the Structuret</h2>
                <p>
                    The building had almost 40 years behind it — uneven slabs,
                    worn-out walls, and quirks that only time can carve. Instead
                    of fighting its age, we worked with it. We kept what held
                    strong, strengthened what had given up, and let go of what
                    no longer made sense. The goal wasn’t to force it into
                    looking new, but to help it stand true , steady, usable, and
                    quietly confident in its own lived-in history. The entire
                    project was delivered within a ₹40L budget, without
                    shortcuts. This was achieved by using high-performing
                    natural materials, lean planning, and smart structure , not
                    by stripping down experience.
                </p>
            </div>
        </div> -->

        <div class="section-4">
            <div class="video-carousel">
                <div class="carousel-container">
                    <!-- Slide 1 -->
                    <div
                        class="carousel-slide {slideIndex === 1
                            ? 'active'
                            : ''}"
                    >
                        <div class="video-component">
                            <div class="video-container">
                                <div
                                    class="video-placeholder"
                                    on:click={() =>
                                        openVideoLightbox("/hrscrollv1.mp4")}
                                    role="button"
                                    tabindex="0"
                                >
                                    <img
                                        src="/Rectangle 58.png"
                                        alt="Video thumbnail"
                                        class="video-thumbnail"
                                    />
                                </div>
                            </div>
                            <div class="video-content">
                                <div>
                                    <h3>The space just felt mine,</h3>
                                    <p class="video-subtitle">
                                        What I had in mind.
                                    </p>
                                </div>
                                <p class="video-description">
                                    Everyone who walks into the studio
                                    compliments the space and for my team, it's
                                    a place that inspires, supports focus, and
                                    feels like somewhere they belong.
                                </p>
                                <div class="video-author">
                                    <p class="author-name">
                                        Himanshu Singh, Founder & COO
                                    </p>
                                    <p class="company-name">
                                        Mouse & Cheese Design Studio
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 2 -->
                    <div
                        class="carousel-slide {slideIndex === 2
                            ? 'active'
                            : ''}"
                    >
                        <div class="video-component">
                            <div class="video-container">
                                <div
                                    class="video-placeholder"
                                    on:click={() =>
                                        openVideoLightbox(
                                            "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                                        )}
                                    role="button"
                                    tabindex="0"
                                >
                                    <img
                                        src="/v234.png"
                                        alt="Video thumbnail"
                                        class="video-thumbnail"
                                    />
                                </div>
                            </div>
                            <div class="video-content">
                                <h3>
                                    It’s a workspace that truly matches the
                                    precision we stand for.
                                </h3>

                                <p class="video-description">
                                    The new office brings clarity and structure
                                    into our everyday operations. Every zone,
                                    whether collaborative or private, has been
                                    thoughtfully designed to support how our
                                    engineering team works.
                                </p>
                                <div class="video-author">
                                    <p class="author-name">
                                        Pawan Panchpal, Founder
                                    </p>
                                    <p class="company-name">
                                        SixD Engineering Solutions
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 3 -->
                    <div
                        class="carousel-slide {slideIndex === 3
                            ? 'active'
                            : ''}"
                    >
                        <div class="video-component">
                            <div class="video-container">
                                <div
                                    class="video-placeholder"
                                    on:click={() =>
                                        openVideoLightbox(
                                            "https://vimeo.com/76979871",
                                        )}
                                    role="button"
                                    tabindex="0"
                                >
                                    <img
                                        src="/v46823.png"
                                        alt="Video thumbnail"
                                        class="video-thumbnail"
                                    />
                                </div>
                            </div>
                            <div class="video-content">
                                <h3>
                                    It’s a home that reflects the elegance we
                                    always imagined
                                </h3>

                                <p class="video-description">
                                    Every corner of the space carries a quiet
                                    sense of luxury, subtle, warm, and
                                    beautifully curated. The aesthetics feel
                                    effortless, yet every detail has been
                                    thoughtfully designed to match our
                                    lifestyle.
                                </p>
                                <div class="video-author">
                                    <p class="author-name">
                                        Ashutosh Sehrawat, Co-Founder
                                    </p>
                                    <p class="company-name">Research Realm</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="carousel-dots">
                    <button
                        class="dot {slideIndex === 1 ? 'active' : ''}"
                        on:click={() => currentSlide(1)}
                    ></button>
                    <button
                        class="dot {slideIndex === 2 ? 'active' : ''}"
                        on:click={() => currentSlide(2)}
                    ></button>
                    <button
                        class="dot {slideIndex === 3 ? 'active' : ''}"
                        on:click={() => currentSlide(3)}
                    ></button>
                </div>
            </div>
        </div>

        <div class="content-2">
            <h3>The Archideus Journal</h3>
            <div class="content-2-description">
                <p>
                    Dive into our thoughts, process, and inspirations. From
                    design insights to behind-the-scenes stories — explore how
                    we think, build, and imagine at Archideus
                </p>
                <a href="/Archideus Journal">
                    <button> Read Our stories </button>
                </a>
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
                                    Concrete, Steel, and Wood Still Reign in
                                    Modern Architecture
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
                                    The Craft of Matter: How Material Choice
                                    Tells a Story in Architecture
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
           <a href="/contact">
 <button>Just Say Hello</button>
       </a>
        </div>
    </div>
</div>

<!-- Video Lightbox Modal -->
<div class="modal fade" id="videoLightbox" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-xl">
        <div class="modal-content bg-black">
            <button
                type="button"
                class="btn-close btn-close-white ms-auto me-2 mt-2"
                data-bs-dismiss="modal"
                aria-label="Close"
            ></button>
            <div
                class="ratio ratio-16x9"
                id="videoWrapper"
                style="border-radius: 0.5rem; overflow: hidden;"
            >
                <!-- JS will inject iframe or video here -->
            </div>
        </div>
    </div>
</div>

<style>
    .case-study-wrapper {
        background-image: url("/bg.png");
        background-repeat: repeat;
        width: 100%;
        min-height: 100vh;
        overflow-x: hidden;
    }
    .container {
        display: flex;
        flex-direction: column;
        width: 100%;
        max-width: 100vw;
        min-height: 100vh;
        align-items: center;
        justify-content: start;
        background-image: url("/bg.png");
        background-repeat: repeat;
        padding-bottom: 10vmax;
        /* Remove these specific overrides that conflict with navbar */
        padding-left: 0;
        padding-right: 0;
        margin: 0;
        box-sizing: border-box;
    }

    .hero-bg {
        margin-top: 0%;
        background-image: url("/image 89.png");
        /* background-color: aqua; */
        background-size: cover;
        background-position: center;
        width: 100vw;
        height: 100vh;
        display: flex;
        align-items: flex-end;
        justify-content: flex-end;
        color: white;
        text-align: center;
        padding-bottom: 4.27vmax;
    }

    .hero-bg div {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 0vmax 5vmax;
    }

    .hero-bg h1 {
        color: #fff;
        width: 48.68vmax;
        min-height: 11.11vmax;
        display: flex;
        padding: 0vmax 5vmax;
        justify-content: center;
        align-content: center;
        text-align: center;
        font-family: var(--font-playfair);
        font-size: 4.16vmax;
        font-style: normal;
        font-weight: 500;
        line-height: 5.59vmax;
        margin-bottom: 0%;
        letter-spacing: -1px;
    }

    .hero-bg p {
        color: #fff;
        font-family: var(--font-instrument);
        font-size: 1.65vmax;
        font-style: normal;
        font-weight: 500;
        line-height: 2.23vmax;
        margin-bottom: 0%;
    }

    .sub-head {
        margin-top: 9.9vmax;
        display: flex;
        width: 90%;
        padding: 1.11vmax 0;
        flex-direction: row;
        justify-content: space-between;
        align-items: start;
        gap: 40px;
    }

    .sub-head h2 {
        color: var(--Accent, #171717);
        font-family: "Instrument Sans";
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        width: 33%;
        line-height: 40px;
        letter-spacing: -0.8px;
    }

    .sub-head p {
        color: var(--Accent, #171717);
        text-align: start;
        font-family: "Instrument Sans";
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 30px;
        width: 58%;
        letter-spacing: -0.38px;
    }

    @media (max-width: 1024px) {
        .hero-bg {
            height: 70vh;
            padding-bottom: 6vmax;
        }

        .hero-bg h1 {
            width: 80%;
            font-size: 3.2vmax;
            line-height: 4.2vmax;
            padding: 0 2vmax;
        }

        .hero-bg p {
            font-size: 1.8vmax;
            line-height: 2.5vmax;
            padding: 0 2vmax;
        }

        .sub-head {
            flex-direction: column;
            align-items: flex-start;
            gap: 2vmax;
        }

        .sub-head h2,
        .sub-head p {
            width: 100%;
            font-size: 24px;
            line-height: 32px;
        }
    }

    @media (max-width: 768px) {
        .hero-bg {
            height: 60vh;
            padding-bottom: vmax;
            justify-content: center;
            text-align: center;
            gap: 0;
        }

        .hero-bg h1 {
            width: 95%;
            font-size: 4vmax;
            padding-bottom: 0px;
            margin-bottom: 0px;
        }

        .hero-bg p {
            padding-top: 0px;
            margin-top: 0px;
            width: 90%;
            font-size: 4vw;
            line-height: 5.5vw;
            padding: 0;
        }

        .sub-head {
            flex-direction: column;
            align-items: center;
            width: 95%;
            text-align: center;
        }

        .sub-head h2 {
            font-size: 22px;
            line-height: 28px;
            width: 100%;
        }

        .sub-head p {
            color: #1e1e1e;
            font-family: "Instrument Sans";
            font-size: 20px;
            font-style: normal;
            font-weight: 400;
            line-height: 30px;
            text-align: start;
            line-height: 30px;
            /* 150% */
            letter-spacing: -0.38px;
        }
    }

    .section-2 {
        display: flex;
        flex-wrap: wrap;
        width: 90%;
        padding: 1.11vmax 0;
        justify-content: space-between;
        align-items: flex-start;
        gap: 1px;
        row-gap: 1vmax;
        margin-top: 20px;
    }

    .section-2 img {
        min-width: 29vmax;
        max-width: 429px;
        max-height: 366px;
        flex-shrink: 0;
        border-radius: 12px;
    }

    @media (max-width: 1024px) {
        .section-2 img {
            width: 48%;
            height: auto;
        }
    }

    @media (max-width: 768px) {
        .section-2 {
            justify-content: center;
        }

        .section-2 img {
            width: 100%;
            height: auto;
        }
    }

    .sub-head-2 {
        margin-top: 7.9vmax;
        display: flex;
        width: 90%;
        padding: 1.11vmax 0;
        flex-direction: row;
        justify-content: space-between;
        align-items: start;
        gap: 40px;
    }

    .sub-head-2 h2 {
        color: #1e1e1e;
        width: 39.58vmax;
        font-family: "Instrument Sans";
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        line-height: 40px;
        letter-spacing: -0.8px;
    }

    .horizontal-scroll {
        display: flex;
        overflow-x: auto;
        overflow-y: hidden;
        gap: 5vmax;
        padding: 10px 0;
        scroll-behavior: auto;
        width: 90%;
        height: 662px;
        align-items: start;
        margin: 0 auto;
        -webkit-overflow-scrolling: touch;
        scroll-snap-type: none;
        scrollbar-width: none;
        -ms-overflow-style: none;
        will-change: scroll-position;
        transform: translateZ(0);
    }

    .horizontal-scroll::-webkit-scrollbar {
        display: none;
    }

    .scroll-item-1 {
        flex: 0 0 auto;
        width: fit-content;
        max-width: 100%;
        border-radius: 12px;
        display: flex;
        flex-direction: row-reverse;
        align-items: center;
        gap: 3vmax;
    }

    .scroll-image {
        height: 536px;
        width: auto;
        min-width: 800px;
        object-fit: cover;

        border-radius: 12px;
    }
    .scroll-image-3 {
        height: 536px;
        width: 500px;
        min-width: 400px;
        object-fit: cover;
        border-radius: 12px;
    }

    .scroll-item-1 p {
        color: #1e1e1e;
        font-family: "Instrument Sans";
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 30px;
        text-align: start;
        line-height: 30px;
        /* 150% */
        letter-spacing: -0.38px;
        /* text-justify: inter-word; */
    }

    .scroll-item-2 {
        flex: 0 0 auto;
        width: 414px;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: start;
        justify-content: flex-start;
        gap: 1vmax;
    }

    .scroll-video {
        width: 100%;
        height: 552px;
        object-fit: cover;
    }

    .video-overlay {
        color: #1e1e1e;
        font-family: "Instrument Sans";
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 30px;
        letter-spacing: -0.38px;
    }

    .scroll-item-3 {
        flex: 0 0 auto;
        max-width: 340px;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: start;
        justify-content: start;
        gap: 1vmax;
    }

    .scroll-item-3 h3 {
        color: #1e1e1e;
        font-family: "Instrument Sans";
        font-size: 32px;
        font-style: normal;
        font-weight: 500;
        line-height: 32px;
        letter-spacing: -0.32px;
        margin-bottom: 0;
        margin-top: 4vmax;
    }

    .scroll-item-3 p {
        color: var(--Accent, #171717);
        text-align: justify;
        font-family: "Instrument Sans";
        font-size: 18px;
        font-style: normal;
        font-weight: 400;
        line-height: 27px;
        text-justify: inter-word;
    }

    .scroll-item-4 {
        flex: 0 0 auto;
        width: 319px;
        display: flex;
        flex-direction: column;
        gap: 1vmax;
    }

    .scroll-item-4 img {
        width: 100%;
        height: 300px;
        border-radius: 12px;
        display: block;
    }

    .scroll-item-5 {
        width: 800px;
        border-radius: 12px;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1vmax;
    }

    .scroll-item-5 img {
        width: 779px;
        height: 536px;
        border-radius: 12px;
    }

    @media (max-width: 1080px) {
        .horizontal-scroll {
            display: flex;
            flex-direction: column;
            overflow-x: hidden;
            overflow-y: visible;
            gap: 2vmax;
            width: 100%;
            height: auto;
            padding: 0 1rem;
        }

        .scroll-video {
            width: auto;
            height: 552px;
            max-height: 90vh;
            object-fit: cover;
        }

        .scroll-item-1,
        .scroll-item-2,
        .scroll-item-3,
        .scroll-item-4,
        .scroll-item-5 {
            flex: unset;
            width: 100%;
            max-width: 100%;
            height: auto;
        }

        .scroll-image,
        .scroll-video,
        .scroll-item-4 img,
        .scroll-item-5 img {
            width: 100%;
            height: auto;
            max-width: 100%;
        }

        .scroll-item-1 {
            flex-direction: column;
            gap: 1rem;
            align-items: flex-start;
        }

        .scroll-item-3 h3 {
            margin-top: 2rem;
        }

        .scroll-item-1 p {
            /* background-color: aqua; */
            text-align: left !important;
            /* override justify */
            text-justify: auto;
            /* reset from inter-word */
            line-height: 30px;
            letter-spacing: -0.38px;
        }
    }

    .hero-bg-2 {
        background-size: cover;
        background-position: center center;
        background-repeat: no-repeat;
        border-radius: 12px;
        width: 100%;
        height: 45.48vmax;
        display: flex;
        align-items: flex-end;
        justify-content: center;
        color: white;
        text-align: center;
        padding: 2rem;
        margin-top: 2vmax;
        position: relative;
        overflow: hidden;
        animation: changeBackground 15s infinite;
    }

    .hero-2 {
        width: 90%;
    }

    @keyframes changeBackground {
        0%,
        20% {
            background-image: url("/1 29.png");
        }

        20.1%,
        40% {
            background-image: url("/BACK SIDE (MASTER BEDROOM)-02 1.png");
        }

        40.1%,
        60% {
            background-image: url("/BACK BATHROOM  1.png");
        }
        60.1%,
        80% {
            background-image: url("/BACK SIDE (MASTER BEDROOM) 1.png");
        }

        80.1%,
        100% {
            background-image: url("/PARENT BEDROOM_01 1.png");
        }
    }

    .hero-bg-2 .animated-text {
        position: relative;
        width: 100%;
        height: auto;
    }

    .hero-bg-2 .animated-text p {
        color: #000;
        text-align: center;
        font-family: "Playfair Display";
        font-size: 3.4vmax;
        font-style: normal;
        font-weight: 500;
        line-height: 56px;
        letter-spacing: -1px;
        position: absolute;
        left: 0;
        right: 0;
        bottom: 20px;
        opacity: 0;
        transform: translateY(29px);
        transition:
            opacity 0.5s ease,
            transform 0.5s ease;
    }

    .hero-bg-2 .text-1 {
        animation: showText1 10s infinite;
    }

    .hero-bg-2 .text-2 {
        animation: showText2 10s infinite;
    }

    .hero-bg-2 .text-3 {
        animation: showText3 10s infinite;
    }

    @keyframes showText1 {
        0%,
        20% {
            opacity: 1;
        }

        20%,
        100% {
            opacity: 0;
        }
    }

    @keyframes showText2 {
        0%,
        20% {
            opacity: 0;
            color: white;
        }

        20%,
        60% {
            opacity: 1;
            color: white;
        }

        60%,
        80% {
            opacity: 0;
        }
    }

    @keyframes showText3 {
        0%,
        60% {
            opacity: 0;
            color: white;
        }

        60%,
        100% {
            opacity: 1;
            color: white;
        }
    }

    .section-4 {
        width: 90%;
        margin-top: 7.9vmax;
        display: flex;
        border-radius: 16px;
        background: url("/bg3.png") no-repeat center center;
        background-size: cover;
        max-width: 90%;
        justify-content: center;
        height: 35vmax;
    }

    .section-3 {
        width: 90%;
        margin-top: 7.9vmax;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 4vmax;
        padding: 2rem 0;
    }

    .section-3-video {
        width: 30vmax;
        height: 41vmax;
        object-fit: cover;
        border-radius: 12px;
    }

    .section-3-card {
        width: 41vmax;
        height: 41vmax;
        flex-shrink: 0;
        border-radius: 8px;
        background: var(--Primary, #8b3a3a);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 3rem;
        text-align: center;
        gap: 2rem;
    }

    .section-3-card h2 {
        color: var(--Secondary, #efe8db);
        text-align: center;
        font-family: "Instrument Sans";
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        line-height: 40px;
        letter-spacing: -0.8px;
        margin: 0;
    }

    .section-3-card p {
        color: var(--Secondary, #efe8db);
        text-align: justify;
        font-family: "Instrument Sans";
        font-size: 20px;
        line-height: 30px;
        letter-spacing: -0.38px;
        margin: 0;
        text-justify: inter-word;
    }

    @media (max-width: 1024px) {
        .section-3 {
            flex-direction: column;
            gap: 3rem;
        }

        .section-3-video {
            width: 80%;
            height: auto;
        }

        .section-3-card {
            width: 85%;
            height: auto;
            padding: 2rem;
        }

        .section-3-card h2 {
            font-size: 32px;
            line-height: 38px;
        }

        .section-3-card p {
            font-size: 18px;
            line-height: 28px;
        }
    }

    @media (max-width: 600px) {
        .section-3 {
            flex-direction: column-reverse;
            gap: 2rem;
            padding: 1.5rem 0;
        }

        .section-3-video {
            width: 100%;
            height: auto;
            max-height: 500px;
            border-radius: 8px;
        }

        .section-3-card {
            width: 100%;
            height: auto;
            padding: 1.5rem;
            border-radius: 6px;
        }

        .section-3-card h2 {
            font-size: 24px;
            line-height: 32px;
        }

        .section-3-card p {
            font-size: 16px;
            line-height: 24px;
        }
    }

    .video-carousel {
        width: 100%;
        position: relative;
    }

    .carousel-container {
        position: relative;
        overflow: hidden;
        border-radius: 16px;
        height: 100%;
    }

    .carousel-slide {
        display: none;
        width: 100%;
    }

    .carousel-slide.active {
        display: flex;
        width: 100%;
        height: 100%;
        justify-content: center;
        align-items: center;
    }

    .video-component {
        display: flex;
        width: 100%;
        justify-content: center;
        align-items: center;
        column-gap: 4vmax;
        border-radius: 16px;
        overflow: hidden;
    }

    .video-container {
        flex: 1;
        position: relative;
        max-width: 529px;
        height: 27vmax;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .video-container img {
        border-radius: 12px;
    }

    .video-placeholder {
        position: relative;
        width: 100%;
        height: 100%;
        cursor: pointer;
    }

    .video-thumbnail {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .play-button {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        cursor: pointer;
        transition: transform 0.2s ease;
    }

    .play-button:hover {
        transform: translate(-50%, -50%) scale(1.1);
    }

    .video-content {
        flex: 1;
        padding: 3rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        gap: 2vmax;
        max-width: 560px;
    }

    .video-content h3 {
        color: #171717;
        font-family: "Playfair Display";
        font-size: 32px;
        font-style: normal;
        font-weight: 400;
        line-height: 133.327%;
        letter-spacing: -0.96px;
    }

    .video-subtitle {
        color: #171717;
        font-family: "Playfair Display";
        font-size: 32px;
        font-style: italic;
        font-weight: 400;
        line-height: 133.327%;
        letter-spacing: 0.32px;
    }

    .video-description {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 18px;
        font-style: normal;
        font-weight: 400;
        line-height: 24px;
        letter-spacing: 0.18px;
    }

    .video-author {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 122.024%;
        letter-spacing: 0.16px;
    }

    .author-name {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 122.024%;
        letter-spacing: 0.16px;
    }

    .company-name {
        color: #171717;
        font-family: "Instrument Sans";
        font-size: 0.9rem;
        font-weight: 400;
        opacity: 0.7;
        letter-spacing: -0.1px;
    }

    .carousel-dots {
        position: absolute;
        bottom: 1rem;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 12px;
        z-index: 10;
    }

    .dot {
        width: 12px;
        height: 12px;
        border-radius: 50%;
        border: none;
        background-color: rgba(23, 23, 23, 0.2);
        cursor: pointer;
        transition: all 0.3s ease;
        padding: 0;
    }

    .dot:hover {
        background-color: rgba(23, 23, 23, 0.4);
        transform: scale(1.1);
    }

    .dot.active {
        background-color: #171717;
        transform: scale(1.2);
    }

    @media (max-width: 1024px) {
        .video-component {
            flex-direction: column;
        }

        .video-container {
            min-height: 300px;
        }

        .video-content {
            padding: 2rem;
        }

        .video-content h3 {
            font-size: 2rem;
        }

        .video-subtitle {
            font-size: 1.25rem;
        }
    }

    @media (max-width: 1000px) {
        .section-4 {
            width: 95%;
            margin-top: 5vmax;
            height: auto;
            min-height: 30vmax;
            padding: 1rem;
        }

        .video-carousel {
            width: 100%;
        }

        .carousel-container {
            border-radius: 12px;
            height: auto;
            min-height: 400px;
        }

        .carousel-slide.active {
            flex-direction: column;
            padding: 1.5rem;
        }

        .video-component {
            flex-direction: column;
            column-gap: 0;
            padding: 0;
            align-items: stretch;
        }

        .video-container {
            max-width: 100%;
            min-height: 200px;
            margin-bottom: 1rem;
        }

        .video-thumbnail {
            border-radius: 8px;
        }

        .video-content {
            max-width: 100%;
            padding: 1rem;
            gap: 1rem;
            text-align: left;
        }

        .video-content h3 {
            font-size: 22px;
            line-height: 120%;
            letter-spacing: -0.5px;
        }

        .video-subtitle {
            font-size: 18px;
            line-height: 120%;
            margin-bottom: 0.5rem;
        }

        .video-description {
            font-size: 14px;
            line-height: 150%;
            letter-spacing: 0.1px;
        }

        .video-author {
            padding-top: 1rem;
            border-top: 1px solid rgba(23, 23, 23, 0.15);
        }

        .author-name {
            font-size: 14px;
            font-weight: 600;
        }

        .company-name {
            font-size: 12px;
            opacity: 0.8;
        }

        .carousel-dots {
            bottom: 1rem;
            gap: 8px;
        }

        .dot {
            width: 8px;
            height: 8px;
        }

        .dot.active {
            transform: scale(1.5);
        }

        .play-button svg {
            width: 80px;
            height: 80px;
        }
    }

    @media (max-width: 480px) {
        .section-4 {
            width: 98%;
            padding: 0.5rem;
            margin-top: 4vmax;
        }

        .carousel-slide.active {
            padding: 1rem;
        }

        .video-container {
            min-height: 180px;
        }

        .video-content {
            padding: 0.8rem;
            gap: 0.8rem;
        }

        .video-content h3 {
            font-size: 20px;
            line-height: 115%;
        }

        .video-subtitle {
            font-size: 16px;
            line-height: 115%;
        }

        .video-description {
            font-size: 13px;
            line-height: 155%;
        }

        .author-name {
            font-size: 13px;
        }

        .company-name {
            font-size: 11px;
        }

        .play-button svg {
            width: 60px;
            height: 60px;
        }

        .carousel-dots {
            bottom: 0.8rem;
            gap: 6px;
        }

        .dot {
            width: 6px;
            height: 6px;
        }
    }

    .content-2 {
        width: 90%;
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 2vmax;
        padding: 0%;
        margin-top: 5vmax;
    }

    .content-2-description {
        display: flex;
        flex-direction: column;
        align-items: start;
        width: 358px;
        height: 100%;
        flex: 0 0 36.8vmax;
        width: 20vmax;
    }

    .content-2 h3 {
        color: var(--Primary, #8b3a3a);
        font-family: "Playfair Display";
        font-size: 4.2vmax;
        font-style: normal;
        font-weight: 400;
        line-height: 64px;
        flex: 1;
        max-width: 50%;
        margin: 0;
        letter-spacing: -1.68px;
    }

    .content-2-description p {
        color: var(--Accent, #171717);
        text-align: justify;
        font-family: "Instrument Sans";
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 30px;
        width: 100%;
        letter-spacing: -0.38px;
    }

    .content-2-description button {
        color: #fff;
        font-family: "Instrument Sans";
        font-size: 20px;
        padding: 1vmax 2.5vmax;
        font-style: normal;
        font-weight: 600;
        line-height: 122.024%;
        letter-spacing: 0.2px;
        border-radius: 56px;
        height: 52px;
        display: flex;
        justify-content: center;
        align-content: center;
        align-items: center;
        width: 281px;
        background: var(--Primary, #8b3a3a);
        border: none;
        outline: none;
    }

    .content-3 {
        display: flex;
        flex-direction: row;
        width: 90%;
        justify-content: space-between;
        padding-top: 5vmax;
        gap: 2vmax;
    }

    .content-3-card {
        flex: 1;
        width: 28vmax;
        display: flex;
        flex-direction: column;
        height: 423px;
    }

    .content-3-card-image {
        position: relative;
        width: 100%;
        height: fit-content;
    }

    .content-3-image1 {
        display: block;
        width: 100%;
        height: 258px;
        object-fit: cover;
    }

    .content-3-image2 {
        position: absolute;
        top: 10px;
        right: 10px;
        width: 24px;
        height: 24px;
        cursor: pointer;
    }

    .content-3-tab {
        display: flex;
        width: 66%;
        flex-direction: row;
        justify-content: space-between;
        gap: 2vmax;
        align-items: stretch;
    }

    .content-3-card-header {
        padding-top: 1.5vmax;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 0%;
    }

    .content-3-card-header h4 {
        font-family: "Instrument Sans";
        font-size: 24px;
        font-style: normal;
        font-weight: 600;
        line-height: 32px;
        margin: 0;
        width: 60%;
        margin-bottom: 0%;
    }

    .content-3-card-header span {
        font-family: "Instrument Sans";
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 24px;
        margin-bottom: 0%;
    }

    .content-3-card-description {
        color: var(--Accent, #171717);
        margin-top: 0;
        width: 82%;
        padding-top: 0%;
        margin-top: 0%;
        margin-bottom: 0%;
        font-family: "Instrument Sans";
        font-size: 18px;
        font-style: normal;
        font-weight: 400;
        line-height: 27px;
        letter-spacing: -0.342px;
    }

    @media (min-width: 800px) and (max-width: 1000px) {
        .content-4 {
            margin-top: 5vmax;
        }
    }

    @media (max-width: 800px) {
        .content-2 {
            flex-direction: column;
            justify-content: start;
            align-items: start;
            gap: 0;
        }

        .content-2 h3 {
            margin-bottom: 0;
        }

        .content-2-description {
            flex-direction: column;
            justify-content: start;
            align-items: start;
            gap: 1vmax;
            width: 100%;
            padding-top: 0;
            margin-top: 0%;
        }

        .content-3-card {
            flex: 1;
            max-width: none;
            min-width: 300px;
        }

        .content-3-tab {
            flex-direction: column;
            gap: 4vmax;
            width: 100%;
        }
    }

    .content-4 {
        display: flex;
        flex-direction: column;
        justify-content: start;
        align-items: start;
        align-content: start;
        width: 90%;
        gap: 2vmax;
        margin-top: 5vmax;
    }

    .content-4 h3 {
        color: var(--Primary, #8b3a3a);
        font-family: "Playfair Display";
        font-size: 4vmax;
        font-weight: 400;
        line-height: 133.327%;
        letter-spacing: -1.2px;
        width: 100%;
        margin-bottom: 0%;
    }

    .content-4 h3 span {
        display: block;
    }

    .itallic {
        font-style: italic;
    }

    .content-4 button {
        color: #fff;
        width: 252px;
        height: 52px;
        display: flex;
        justify-content: center;
        align-content: center;
        align-items: center;
        font-family: "Instrument Sans";
        font-size: 20px;
        font-style: normal;
        font-weight: 600;
        line-height: 122.024%;
        letter-spacing: 0.2px;
        border-radius: 56px;
        background: #8b3a3a;
        border: none;
        outline: none;
    }

    @media (max-width: 700px) {
        .content-4 h3 {
            width: 80%;
        }

        .content-2 {
            flex-direction: column;
            justify-content: start;
            align-items: start;
            gap: 0;
            margin-top: 2rem;
        }

        .content-2 h3 {
            margin-bottom: 0;
            width: 100%;
            max-width: 100%;
        }

        .content-2-description {
            flex-direction: column;
            justify-content: start;
            align-items: start;
            gap: 1vmax;
            width: 100%;
            padding-top: 0;
            margin-top: 0%;
        }

        .content-3 {
            flex-direction: column;
            gap: 2rem;
        }

        .content-3-tab {
            flex-direction: column;
            gap: 2rem;
            margin-bottom: 0;
            width: 100%;
        }

        .content-4 h3 {
            width: 100%;
            margin-top: 3rem;
        }

        .content-3-card {
            flex: none;
            max-width: none;
            min-width: auto;
            width: 100%;
            height: auto;
        }
    }

    /* Bootstrap Modal Overrides */
    .modal {
        z-index: 9999;
    }

    .modal-content {
        background-color: #000;
    }

    .btn-close-white {
        filter: invert(1) grayscale(100%) brightness(200%);
    }

    .ratio {
        position: relative;
    }

    .ratio::before {
        content: "";
        display: block;
        padding-top: 56.25%;
    }

    .ratio > * {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
</style>
