<script>
    import { onMount } from "svelte";
    let isInView = false;
    let textEl;

    onMount(() => {
        const observer = new IntersectionObserver(
            ([entry]) => {
                isInView = entry.isIntersecting;
            },
            { threshold: 0.5 },
        );
        if (textEl) {
            observer.observe(textEl);
        }
    });
</script>

<section class="heroTxt">
    <div class="mask-container">
        <p class="masked-text" bind:this={textEl} class:animate={isInView}>
            <span class="word-box"><span>Following</span></span>
            <span class="word-box"><span>what</span></span>
            <span class="word-box"><span>matters</span></span>
        </p>
    </div>
</section>

<style>
    .heroTxt {
        position: relative;
        width: 100vw;
        height: 100vh;
        min-height: 400px;
        display: flex;
        overflow: hidden;
        background-color: var(--primary);
        align-items: center;
        justify-content: center;
    }

    .mask-container {
        overflow: hidden;
        display: inline-block;
        width: 70%;
        text-align: center;
        max-width: 970px;
    }

    .masked-text {
        display: flex;
        flex-wrap: wrap;
        gap: 0.8rem;
        font-size: 2.5rem;
        font-weight: bold;
        color: #fff;
        font-family: sans-serif;
        align-items: center;
        justify-content: center;
        line-height: 65px;
        padding-bottom: 10px;
    }

    .word-box {
        display: inline-block;
        background-color: var(--primary); /* match the section bg */
        overflow: hidden;
        height: 4.5rem; /* match font size approx */
        line-height: 2.5rem;
        vertical-align: bottom;
        padding: 0 4px;
        border-radius: 4px;
        gap: 0.8rem;
        line-height: 65px;
        padding-bottom: 10px;
        font-family: var(--main);
        font-size: 162%;
        font-weight: 400;
    }

    .word-box span {
        display: inline-block;
        transform: translateY(100%);
        opacity: 0;
    }

    .animate .word-box span {
        animation: riseUp 0.5s ease-out forwards;
    }

    .animate .word-box:nth-child(1) span {
        animation-delay: 106ms;
    }
    .animate .word-box:nth-child(2) span {
        animation-delay: 206ms;
    }
    .animate .word-box:nth-child(3) span {
        animation-delay: 312ms;
    }

    @keyframes riseUp {
        0% {
            transform: translateY(100%);
            opacity: 0;
        }
        100% {
            transform: translateY(0%);
            opacity: 1;
        }
    }

    @media (max-width: 768px) {
        .heroTxt {
            height: 60vh;
        }

        .mask-container {
            width: 90%;
        }

        .masked-text {
            font-size: 2.3rem;
            gap: 0.6rem;
            line-height: 60px;
            padding-bottom: 0;
        }

        .word-box {
            height: 4rem;
            line-height: 60px;
            font-size: 155%;
            padding: 0 3px;
        }
    }

    @media (max-width: 480px) {
        .heroTxt {
            height: 50vh;
        }

        .masked-text {
            font-size: 2rem;
            line-height: 50px;
        }

        .word-box {
            height: 3.2rem;
            line-height: 50px;
            font-size: 140%;
        }
    }
</style>
