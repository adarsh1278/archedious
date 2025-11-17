<script>
    import { onMount } from "svelte";

    let visible = false;
    let container;

    function setupObserver(el, setVisible) {
        const observer = new IntersectionObserver(
            (entries) => {
                const entry = entries[0];
                if (entry.isIntersecting) {
                    setTimeout(() => {
                        if (entry.isIntersecting) setVisible(true);
                    }, 100);
                } else {
                    setVisible(false);
                }
            },
            { threshold: 0.7 },
        );

        if (el) observer.observe(el);
        return () => observer.disconnect();
    }

    onMount(() => {
        const cleanup = setupObserver(container, (v) => (visible = v));

        // Swiper init with autoplay
        new Swiper(".mySwiper", {
            cssMode: true,
            navigation: {
                nextEl: ".swiper-button-next",
                prevEl: ".swiper-button-prev",
            },
            pagination: {
                el: ".swiper-pagination",
            },
            mousewheel: true,
            keyboard: true,
            autoplay: {
                delay: 5000, // 5 sec per slide
                disableOnInteraction: false, // user navigate kare tab bhi autoplay continue rahe
            },
            loop: true, // infinite loop
        });

        return () => cleanup();
    });
</script>

<!-- Swiper CSS -->
<link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css"
/>

<section bind:this={container}>
    <h1 class="title">See What We Build</h1>

    <div class="inner-box {visible ? 'expanded' : 'initial'}">
        <div class="swiper mySwiper">
            <div class="swiper-wrapper">
                <div class="swiper-slide">
                    <a href="/casestudies/roopnagar">
                        <h2>Roop nagar villa</h2>
                        <span>Residential | Noida, Uttar Pradesh</span>
                        <img src="/FINAL 1.png" width="100%" />
                    </a>
                </div>

                <div class="swiper-slide">
                    <a href="/casestudies/mouseAndcheese">
                        <h2 id="nmsmjk">Mouse and cheese design studio</h2>
                        <span>Commercial | Noida, Uttar Pradesh</span>

                        <img src="2.png" width="100%" />
                    </a>
                </div>
                <div class="swiper-slide">
                    <a href="/casestudies/DIRECTOR CABIN LOUNGE  1.png">
                        <h2 id="nmsmjk">office-Space</h2>
                        <span>Commercial | Noida, Uttar Pradesh</span>

                        <img src="2.png" width="100%" />
                    </a>
                </div>

                <a class="swiper-slide" href="/casestudies/Lawrence">
                    <h2>Laurence Duplex</h2>
                    <img src="/case2.png" width="100%" />
                    <span>Residential | Noida, Uttar Pradesh</span>
                </a>
            </div>
            <div class="swiper-button-next"></div>
            <div class="swiper-button-prev"></div>
            <div class="swiper-pagination"></div>
        </div>
    </div>
</section>

<style>
    section {
        width: 100%;
        height: 100dvh;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        margin: 100px 0px;
        flex-direction: column;
    }

    .title {
        text-align: left;
        width: 100%;
        padding-left: 58px;
        padding-bottom: 20px;
    }

    .swiper-slide {
        position: relative;
        text-align: center;
        background: #444;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .swiper-slide h2 {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 4.8rem;
        color: #fff;
        text-align: center;
        font-weight: 500;
        line-height: 1.2;

        width: 100%;
    }

    .swiper-slide span {
        position: absolute;
        top: 51%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 24px;
        color: #fff;
        text-align: center;
        font-weight: 500;
        line-height: 1.2;
        width: 100%;
        margin-top: 65px;
    }

    .swiper-button-next,
    .swiper-button-prev {
        color: white !important;
        opacity: 1 !important;
    }

    .swiper-button-next.swiper-button-disabled,
    .swiper-button-prev.swiper-button-disabled {
        color: white !important;
        opacity: 1 !important;
    }

    .swiper-button-next,
    .swiper-rtl .swiper-button-prev,
    .swiper-button-prev,
    .swiper-rtl .swiper-button-next {
        background-color: #ffffff5e;
        width: 50px !important;
        height: 50px !important;
        border-radius: 50%;
        opacity: 1 !important;
        right: 55px;
    }

    .swiper-button-prev {
        left: 55px;
    }

    .swiper-button-next:after,
    .swiper-button-prev:after {
        font-size: 22px !important;
    }

    .inner-box {
        background: gray;
        transition: all 600ms ease-in-out;
        overflow: hidden;
    }

    .initial {
        width: 1322px;
        height: 622px;
    }

    .expanded {
        width: 100%;
        height: 100%;
    }

    /* Swiper full inside */
    .swiper {
        width: 100%;
        height: 100%;
    }

    .swiper-slide {
        text-align: center;
        font-size: 18px;
        background: #444;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .swiper-slide img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    @media (max-width: 768px) {
        section {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            margin: 100px 0px;
            flex-direction: column;
        }

        .initial {
            width: 100%;
            height: 100%;
        }

        .title {
            text-align: left;
            width: 100%;
            padding-left: 28px;
            padding-bottom: 20px;
            font-size: 32px;
        }

        .swiper-slide span {
            position: absolute;
            top: 51%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 21px;
            color: #fff;
            text-align: center;
            font-weight: 500;
            line-height: 1.2;
            width: 100%;
            margin-top: 45px;
        }

        .swiper-slide h2 {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2.5rem;
            color: #fff;
            text-align: center;
            font-weight: 500;
            line-height: 1.2;
            width: 100%;
        }

        .swiper-button-next,
        .swiper-button-prev {
            background-color: #ffffff5e;
            width: 50px !important;
            height: 50px !important;
            border-radius: 50%;
            opacity: 1 !important;
            right: 15px;
        }

        .swiper-button-prev {
            left: 15px !important;
        }

        #nmsmjk {
            font-size: 1.6rem !important;
        }
    }
</style>
