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
            <span>We</span>
            <span>listen,</span>
            <span>understand</span>
            <span>and</span>
            <span>build,</span> <br />
            <span>So</span>
            <span>your</span>
            <span>thoughts</span>
            <span>become</span>
            <span>meaningful</span>
            <span>spaces.</span>
        </p>
    </div>
</section>

<style>
    span {
        font-family: var(--main);
        font-size: 170%;
        font-weight: 400;
    }

    .heroTxt {
        position: relative;
        width: 100vw;
        height: 100vh;
        display: flex;
        overflow: hidden;
        background-color: var(--primary);
        align-items: center;
        justify-content: center;
    }

    .mask-container {
        overflow: hidden;
        display: inline-block;
        width: 67%;
        text-align: center;
        max-width: 965px;
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

    .masked-text span {
        display: inline-block;
        transform: translateY(100%);
        opacity: 0;
    }

    .animate span {
        animation: riseUp 0.5s ease-out forwards;
    }

    .animate span:nth-child(1) {
        animation-delay: 106ms;
    }
    .animate span:nth-child(2) {
        animation-delay: 206ms;
    }
    .animate span:nth-child(3) {
        animation-delay: 312ms;
    }
    .animate span:nth-child(4) {
        animation-delay: 418ms;
    }
    .animate span:nth-child(5) {
        animation-delay: 524ms;
    }
    .animate span:nth-child(6) {
        animation-delay: 630ms;
    }
    .animate span:nth-child(7) {
        animation-delay: 736ms;
    }
    .animate span:nth-child(8) {
        animation-delay: 842ms;
    }
    .animate span:nth-child(9) {
        animation-delay: 948ms;
    }
    .animate span:nth-child(10) {
        animation-delay: 1054ms;
    }
    .animate span:nth-child(11) {
        animation-delay: 1160ms;
    }
    .animate span:nth-child(12) {
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
</style>
