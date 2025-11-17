<script>
    export let heading = "";
    export let description = "";
    export let imageSrc = "";
    export let cardClass = "";
</script>

<div class="section">
    <div class="container {cardClass}" style="z-index : 1">
        <div class="box-wrapper">
            <div class="circle"></div>
            <div class="rect"></div>
            <img class="image" src={imageSrc} alt="" />
        </div>

        <div class="ndkdj">
            <p class="heading">{heading}</p>

            <p class="para">{description}</p>
        </div>
    </div>
</div>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .ndkdj{
        display: flex;
        background-image: url('bg.png');
    }

    html,
    body {
        width: 100%;
        height: 100%;
        margin: 0;
        padding: 0;
    }

    .section {
        width: 100vw;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background-repeat: repeat;
        margin: 0;
        padding: 0;
        z-index: 1;
    }

    .container {
        position: relative;
        width: 100%;
        height: 100%;
        background-repeat: repeat;
        margin: 0 !important;
        padding: 0 !important;
        box-sizing: border-box;
    }

    .box-wrapper {
        position: absolute;
        width: 503px;
        height: 655px;
        top: 48px;
        left: 484px;
    }

    .circle {
        position: absolute;
        width: 110px;
        height: 110px;
        top: 545px;
        left: 393px;
        background: #8b3a3a;
        border-radius: 55px;
    }

    .rect {
        position: absolute;
        width: 295px;
        height: 452px;
        top: 0;
        left: 0;
        background: #8b3a3a;
    }

    .image {
        position: absolute;
        width: 424px;
        height: 576px;
        top: 24px;
        left: 24px;
        object-fit: cover;
    }

    .heading {
        position: absolute;
        width: 400px;
        top: 71px;
        left: 64px;
        font-family: "Playfair Display", Helvetica, serif;
        font-weight: 400;
        font-size: 3rem;
        line-height: 56px;
        letter-spacing: -0.48px;
        color: #8b3a3a;
        background-image: url("bg.png");
    }

    .para {
        position: absolute;
        width: 321px;
        top: 213px;
        left: 64px;
        font-family: "Instrument Sans", sans-serif;
        font-size: 20px;
        font-weight: 400;
        line-height: 28px;
        letter-spacing: 0.2px;
        font-style: normal;
        color: #171717;
        background-image: url("bg.png");
    }

    @media (max-width: 1024px) and (min-width: 769px) {
        .section {
            flex-direction: column;
            padding: 20px;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 40px 20px;
        }

        .box-wrapper {
            position: relative;
            width: 400px;
            height: 520px;
            top: 0;
            left: 0;
            margin-bottom: 30px;
        }

        .circle {
            width: 80px;
            height: 80px;
            top: 440px;
            left: 320px;
            border-radius: 40px;
        }

        .rect {
            width: 240px;
            height: 360px;
            top: 0;
            left: 0;
        }

        .image {
            width: 340px;
            height: 460px;
            top: 20px;
            left: 20px;
        }

        .heading {
            position: relative;
            width: 100%;
            max-width: 400px;
            top: 0;
            left: 0;
            text-align: center;
            font-size: 2.5rem;
            line-height: 48px;
            margin-bottom: 20px;
        }

        .para {
            position: relative;
            width: 100%;
            max-width: 400px;
            top: 0;
            left: 0;
            text-align: center;
            font-size: 18px;
            line-height: 26px;
        }
    }

    /* Mobile styles */
    @media (max-width: 768px) {
        .section {
            height: auto;
            max-width: 100vw !important;
            min-height: 100vh;
            flex-direction: column;
            padding: 20px;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            height: auto;
            min-height: 100vh;
            padding: 20px;
        }

        .box-wrapper {
            position: relative;
            width: 100%;
            max-width: 320px;
            height: 420px;
            top: 0;
            left: 0;
            margin-bottom: 30px;
        }

        .circle {
            width: 60px;
            height: 60px;
            top: 360px;
            left: 260px;
            border-radius: 30px;
        }

        .rect {
            width: 200px;
            height: 300px;
            top: 0;
            left: 0;
        }

        .image {
            width: 280px;
            height: 380px;
            top: 15px;
            left: 15px;
        }

        .heading {
            position: relative;
            width: 100%;
            max-width: 320px;
            top: 0;
            left: 0;
            text-align: center;
            font-size: 2rem;
            line-height: 40px;
            margin-bottom: 20px;
        }

        .para {
            position: relative;
            width: 100%;
            max-width: 320px;
            top: 0;
            left: 0;
            text-align: center;
            font-size: 16px;
            line-height: 24px;
        }
    }

    /* Small mobile styles */
    @media (max-width: 480px) {
        .section {
            background-image: url("/bg.png");
            background-repeat: repeat;
            padding: 15px;
            overflow-x: hidden;
        }

        .container {
            padding: 15px;
        }

        .box-wrapper {
            max-width: 280px;
            height: 360px;
        }

        .circle {
            width: 50px;
            height: 50px;
            top: 310px;
            left: 230px;
            border-radius: 25px;
        }

        .rect {
            width: 170px;
            height: 250px;
        }

        .image {
            width: 240px;
            height: 320px;
            top: 12px;
            left: 12px;
        }

        .heading {
            max-width: 280px;
            font-size: 1.75rem;
            line-height: 36px;
        }

        .para {
            max-width: 280px;
            font-size: 15px;
            line-height: 22px;
        }
    }
</style>
