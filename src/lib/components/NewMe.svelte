<div class="container">
  <div class="text-section">
    <h1>For those who makes it home</h1>
    <p>Your Stories, Your Dreams shaped into spaces that feels like home</p>
  </div>

  <div class="image-section">
    <div class="frame">
      <img src="h1.png" alt="Happy couple at home" />
    </div>
  </div>

  <div class="blank-section"></div>
</div>

<div class="container">
  <div class="text-section">
    <h1>Workspaces that speaks for you</h1>
    <p>
      Designed for performance and people, spaces where your team thrives and
      your vision becomes reality.
    </p>
  </div>

  <div class="image-section">
    <div class="frame">
      <img src="hh2.png" alt="Modern workspace" />
    </div>
  </div>

  <div class="blank-section"></div>
</div>

<div class="container">
  <div class="text-section">
    <h1>For those building something bolder</h1>
    <p>
      Designed to serve, support, and stand for something greater, schools,
      hospitals, and public spaces.
    </p>
  </div>

  <div class="image-section">
    <div class="frame">
      <img src="hh4.png" alt="Public spaces" />
    </div>
  </div>

  <div class="blank-section"></div>
</div>

<style>
  :root {
    --primary-color: #8c3d3d;
    --text-color: #333;
    --max-width: 1300px;
  }

  .text-section > h1 {
    z-index: 3;
    position: relative;
    text-align: left;
  }

  .text-section > p {
    z-index: 3;
    text-align: left;
    position: relative;
  }

  .container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 40px;
    padding: 60px 5%;
    max-width: var(--max-width);
    margin: auto;
    min-height: 90vh;
    box-sizing: border-box;
    flex-wrap: wrap; /* mobile support */
  }

  .text-section {
    flex: 1 1 400px;
  }

  .blank-section {
    flex: 1 1 200px;
  }

  .text-section h1 {
    font-size: clamp(1.8rem, 2.5vw, 3rem);
    font-weight: 600;
    color: var(--primary-color);
    margin: 0 0 20px;
    line-height: 1.2;
  }

  .text-section p {
    font-size: 1rem;
    max-width: 420px;
    line-height: 1.6;
    opacity: 0.9;
  }

  .image-section {
    position: relative;
    flex: 1 1 400px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .frame {
    position: relative;
    overflow: hidden;
    transition: transform 0.4s ease;
    z-index: 3;
  }

  .frame:hover {
    transform: translateY(-5px) scale(1.02);
  }

  .frame img {
    display: block;
    width: 100%;
    max-width: 480px;
    height: auto;
    border-radius: inherit;
    object-fit: cover;
  }

  .circle {
    position: absolute;
    bottom: -40px;
    right: -40px;
    width: 120px;
    height: 120px;
    background: var(--primary-color);
    border-radius: 50%;
    z-index: -1;
    opacity: 0.15;
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
  }
</style>
