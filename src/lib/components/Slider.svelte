<div class="container">
    <div class="section one">
        <img
            src="https://th-thumbnailer.cdn-si-edu.com/zXKdi9i_HHmG07qw1h2l9TyEQYc=/1280x1280/filters:focal(1471x1061:1472x1062)/https://tf-cmsv2-smithsonianmag-media.s3.amazonaws.com/filer/b6/30/b630b48b-7344-4661-9264-186b70531bdc/istock-478831658.jpg"
            height="655"
            width="500"
        />
    </div>

    <div class="section two">
        <img
            src="https://th-thumbnailer.cdn-si-edu.com/zXKdi9i_HHmG07qw1h2l9TyEQYc=/1280x1280/filters:focal(1471x1061:1472x1062)/https://tf-cmsv2-smithsonianmag-media.s3.amazonaws.com/filer/b6/30/b630b48b-7344-4661-9264-186b70531bdc/istock-478831658.jpg"
            height="655"
            width="500"
        />
    </div>
    <div class="section three">
        <img
            src="https://th-thumbnailer.cdn-si-edu.com/zXKdi9i_HHmG07qw1h2l9TyEQYc=/1280x1280/filters:focal(1471x1061:1472x1062)/https://tf-cmsv2-smithsonianmag-media.s3.amazonaws.com/filer/b6/30/b630b48b-7344-4661-9264-186b70531bdc/istock-478831658.jpg"
            height="655"
            width="500"
        />
    </div>
</div>

<style>
    h1 {
        font-size: 48px;
    }

    .container {
        position: absolute;
        width: 100%;
        z-index: 200;
        margin-top: 1130px;
        max-width: unset;
    }

    .section {
        position: sticky;
        top: 0;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 3em;
        color: white;
        font-family: sans-serif;
    }

    .sectionPart {
        width: 100vw;
        height: 100%;
        display: flex;
    }

    .content,
    .img,
    .des {
        height: 100%;
        padding: 40px;
    }

    .content {
        width: 30%;
    }

    .img {
        width: 40%;
        /* background-color: red; */
    }

    .des {
        width: 30%;
        /* background-color: slateblue; */
    }

    .one {
        /* background-color: var(--background); */
        z-index: 1;
    }

    .two {
        /* background-color: var(--background); */

        z-index: 2;
    }

    .three {
        /* background-color: var(--background); */

        z-index: 3;
    }

    .spacer {
        height: 200vh;
        background: #eee;
    }
</style>
