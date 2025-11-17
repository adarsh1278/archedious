<!--
SvelteKit static page: Case Study / Article layout (pure CSS, responsive)
Usage:
 1. Create file: src/routes/case-study/+page.svelte
 2. Copy images into: static/images/
    - hero: /images/case-study-hero.png
    - materials-grid: /images/materials-grid.png  (optional)
    - wood-samples: /images/wood-samples.png
    - steel-tubes: /images/steel-tubes.png
 3. This is a static page, no fetch or JS required.
-->

<script>
  // pure static page — no client-side JS needed for functionality
  export let title = "The Science Behind Timeless Materials: Why Concrete, Steel, and Wood Still Reign in Modern Architecture";
  export let readTime = "5 min read";
</script>

<svelte:head>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>{title}</title>
</svelte:head>

<main class="container">
  <header class="hero">
    <div class="hero-meta">{readTime}</div>
    <h1 class="hero-title">{title}</h1>
    <p class="hero-sub">The Eternal Grammar of Space-Making</p>
  </header>

  <article class="content">
    <section class="lead">
      <p>
        In the relentless pursuit of architectural novelty, we witness an endless parade of new building materials—each promising to revolutionize how we shape space. Yet, like the monsoon that returns each year to renew the earth, three ancient materials continue to define our modern architecture: concrete, steel, and wood. They are the fundamental vocabulary with which we compose the symphony of human habitation.
      </p>
      <figure class="lead-figure" aria-hidden="true">
        <img src="/images/case-study-hero.png" alt="Grid of material samples: concrete, wood, steel, brick"/>
      </figure>
    </section>

    <h2>Concrete: The Alchemy of Modern India</h2>
    <p class="drop">
      <strong>The Poetry of Chemical Transformation</strong>
    </p>
    <p>
      Consider concrete—this miraculous substance that begins as powder and water, yet through an ancient alchemy becomes stone. The concrete hydration process is nothing short of poetic: calcium silicate crystals growing like coral in an invisible sea, binding sand and stone into a matrix stronger than the materials from which it came.
    </p>

    <div class="two-col">
      <div>
        <h3>The Climate-Responsive Wisdom</h3>
        <p>
          Modern concrete technology has learned to dance with India’s extreme climate. Like the thick walls of our traditional architecture, concrete’s thermal mass moderates temperature swings, creating comfortable microclimates within our buildings.
        </p>
      </div>
      <figure>
        <img src="/images/steel-tubes.png" alt="stacked steel hollow tubes"/>
        <figcaption>The Lightness of Being — prefabricated steel sections</figcaption>
      </figure>
    </div>

    <h2>Steel: The Tensile Dreams of Modernity</h2>
    <p>
      <strong>The Structural Poetry of Progress</strong>
    </p>
    <p>
      Steel construction enabled architecture’s great liberation from the tyranny of the wall. No longer did load-bearing masonry dictate the rhythm of openings—steel’s extraordinary strength-to-weight ratio freed façades to become pure expression.
    </p>

    <h2>Wood: The Living Memory of Architecture</h2>
    <p>
      <strong>The Cellular Wisdom of Growth</strong>
    </p>
    <p>
      Wood construction connects us to architecture’s deepest roots. Unlike the manufactured uniformity of concrete and steel, timber construction carries the memory of seasons, the record of rainfall, the signature of soil and sunlight.
    </p>

    <figure class="materials-grid" aria-hidden="true">
      <img src="/images/wood-samples.png" alt="planks of finished wood showing grain and finish"/>
      <figcaption>Timber samples — tactile, warm, and resonant</figcaption>
    </figure>

    <section class="footer-cta">
      <p>Want a responsive SvelteKit template for more articles like this? Copy this file into your project and replace the images in <code>/static/images/</code>.</p>
      <a class="btn" href="#top">Back to top</a>
    </section>
  </article>
</main>

<style>
  :global(html,body){
    height:100%;
    margin:0;
    font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    color: #2b2b2b;
    background: #f7f2ec; /* warm paper */
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
  }

  .container{
    max-width:1100px;
    margin:32px auto;
    padding:24px;
    box-sizing:border-box;
  }

  /* HERO */
  .hero{
    background: linear-gradient(180deg, rgba(0,0,0,0.02), transparent);
    padding:28px 24px;
    border-radius:12px;
    margin-bottom:18px;
  }
  .hero-meta{
    font-size:13px;
    color:#7a5147;
    margin-bottom:8px;
  }
  .hero-title{
    color:#6e2022;
    font-size:28px;
    line-height:1.12;
    margin:0 0 8px 0;
    font-weight:700;
  }
  .hero-sub{
    margin:0;
    color:#3f352f;
    font-weight:600;
  }

  /* ARTICLE */
  .content{
    background: #fff;
    padding:28px;
    border-radius:12px;
    box-shadow: 0 6px 18px rgba(12,12,12,0.04);
  }

  .lead p{
    margin:0 0 18px 0;
    color:#3b3b3b;
    font-size:16px;
    line-height:1.7;
  }

  .lead-figure{
    margin:18px 0 24px 0;
    display:block;
    border-radius:10px;
    overflow:hidden;
  }
  .lead-figure img{width:100%;height:auto;display:block;}

  h2{font-size:20px;margin-top:20px;color:#3b2b2a}
  h3{font-size:16px;margin:0 0 10px 0}

  .drop{
    margin-top:12px;
    margin-bottom:10px;
    color:#6a5849;
  }

  .two-col{
    display:grid;
    grid-template-columns:1fr 340px;
    gap:20px;
    align-items:start;
    margin:18px 0;
  }
  .two-col figure{margin:0;border-radius:8px;overflow:hidden}
  .two-col img{width:100%;height:auto;display:block}
  .two-col figcaption{font-size:13px;color:#6b6b6b;padding-top:6px}

  .materials-grid{margin:26px 0;border-radius:10px;overflow:hidden}
  .materials-grid img{width:100%;height:auto;display:block}
  .materials-grid figcaption{font-size:13px;color:#6b6b6b;padding-top:8px}

  .footer-cta{
    margin-top:28px;
    padding-top:18px;
    border-top:1px solid #eee;
    display:flex;
    justify-content:space-between;
    align-items:center;
    gap:12px;
    flex-wrap:wrap;
  }
  .btn{
    text-decoration:none;
    padding:10px 14px;
    border-radius:8px;
    background:#6e2022;
    color:#fff;
    font-weight:600;
    font-size:14px;
  }

  code{background:#f3f1ef;padding:4px 6px;border-radius:6px;font-size:13px}

  /* Responsive adjustments */
  @media (max-width:900px){
    .container{padding:18px;margin:20px}
    .hero-title{font-size:22px}
    .content{padding:18px}
    .two-col{grid-template-columns:1fr;}
  }

  @media (max-width:480px){
    .hero{padding:18px}
    .hero-meta{font-size:12px}
    .hero-title{font-size:18px}
    .hero-sub{font-size:13px}
    .content{padding:14px}
  }

  /* small polish for images to look crisp on retina */
  img{display:block;max-width:100%;height:auto}

</style>
