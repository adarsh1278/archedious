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
            <span class="word-box"><span>We</span></span>
            <span class="word-box"><span>listen,</span></span>
            <span class="word-box"><span>understand</span></span>
            <span class="word-box"><span>and</span></span>
            <span class="word-box"><span>build,</span></span>
            <span class="word-box"><span>So</span></span>
            <span class="word-box"><span>your</span></span>
            <span class="word-box"><span>thoughts</span></span>
            <span class="word-box"><span>become</span></span>
            <span class="word-box"><span> <i>meaningful</i></span></span>
            <span class="word-box"><span><i>spaces.</i></span></span>
        </p>
    </div>
</section>

<style>
    .heroTxt {
        position: relative;
        width: 100vw;
        height: 100vh;
        display: flex;
        overflow: hidden;
        background-color: var(--primary);
        align-items: center;
        justify-content: center;
        z-index: -3;
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
        background-color: var(--primary);
        overflow: hidden;
        height: 4.5rem; 
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
    .animate .word-box:nth-child(4) span {
        animation-delay: 418ms;
    }
    .animate .word-box:nth-child(5) span {
        animation-delay: 524ms;
    }
    .animate .word-box:nth-child(6) span {
        animation-delay: 630ms;
    }
    .animate .word-box:nth-child(7) span {
        animation-delay: 736ms;
    }
    .animate .word-box:nth-child(8) span {
        animation-delay: 842ms;
    }
    .animate .word-box:nth-child(9) span {
        animation-delay: 948ms;
    }
    .animate .word-box:nth-child(10) span {
        animation-delay: 1054ms;
    }
    .animate .word-box:nth-child(11) span {
        animation-delay: 1160ms;
    }
    .animate .word-box:nth-child(12) span {
        animation-delay: 1266ms;
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
            font-size: 2rem;
            gap: 0.6rem;
            line-height: 50px;
            padding-bottom: 0;
        }

        .word-box {
            height: 3rem;
            line-height: 50px;
            font-size: 140%;
            padding: 0 3px;
        }
    }

    @media (max-width: 480px) {
        .heroTxt {
            height: 50vh;
        }

        .mask-container {
            width: 95%;
        }

        .masked-text {
            font-size: 1.6rem;
            gap: 0.5rem;
            line-height: 42px;
        }

        .word-box {
            height: 2.6rem;
            line-height: 42px;
            font-size: 120%;
        }
    }
</style>
