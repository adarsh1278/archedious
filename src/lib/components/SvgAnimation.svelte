<script lang="ts">
  import { onMount, onDestroy } from "svelte";

  let pathEl: SVGPathElement;
  let wrapperEl: HTMLDivElement;
  let svgEl: SVGSVGElement;

  // Update this if your file sits at a different URL in your project
  const svgFileUrl = "/Homepage- final (1).svg";

  // Auto-scroll/animation params
  const speed = 1.9;
  let triggerPoint = 700;
  let scrollHandler: (() => void) | null = null;

  // Helpers ------------------------------------------------------------
  function pathStartScreenY(pathEl: SVGPathElement | null): number | null {
    if (!pathEl) return null;
    const svg = pathEl.ownerSVGElement;
    if (!svg) return null;
    try {
      const pt = pathEl.getPointAtLength(0);
      const svgRect = svg.getBoundingClientRect();
      const viewBox = svg.viewBox.baseVal;
      const scaleY = svgRect.height / viewBox.height;
      return svgRect.top + pt.y * scaleY;
    } catch (e) {
      return null;
    }
  }

  function setupPathAnimation(
    pathEl: SVGPathElement | null,
  ): number | undefined {
    if (!pathEl) return;
    const length = pathEl.getTotalLength();
    pathEl.style.strokeDasharray = String(length);
    pathEl.style.strokeDashoffset = String(length);
    // expose length for scroll handler via closure
    return length;
  }

  function installScrollHandler(
    pathEl: SVGPathElement,
    pathLength: number,
    svgHeight: number,
  ): (() => void) | null {
    if (!pathEl) return null;

    function handleScroll() {
      const scrollTop = window.scrollY || window.pageYOffset;
      if (scrollTop < triggerPoint) {
        pathEl.style.strokeDashoffset = String(pathLength);
        return;
      }
      const effectiveScroll = scrollTop - triggerPoint;
      const rawPercent = effectiveScroll / (svgHeight - triggerPoint);

      const dynamicSpeed = 1.8 - rawPercent * 0.5;

      const scrollPercent = rawPercent * dynamicSpeed;
      const clamped = Math.max(0, Math.min(scrollPercent, 1));
      pathEl.style.strokeDashoffset = String(pathLength * (1 - clamped));
    }

    window.addEventListener("scroll", handleScroll, { passive: true });
    // run once
    handleScroll();
    return handleScroll;
  }

  // Main mount ---------------------------------------------------------
  onMount(async () => {
    if (typeof window === "undefined") return;

    // fetch new svg file text (encode URI to handle spaces / parens)
    let svgText;
    try {
      const res = await fetch(encodeURI(svgFileUrl));
      if (!res.ok) {
        console.error("Failed to fetch SVG:", res.status, res.statusText);
        return;
      }
      svgText = await res.text();
    } catch (err) {
      console.error("Error fetching SVG:", err);
      return;
    }

    // parse and extract <path> and viewBox / height
    const parser = new DOMParser();
    const doc = parser.parseFromString(svgText, "image/svg+xml");
    const newPathEl = doc.querySelector("path") || doc.querySelector(".cls-1");
    const newSvgEl = doc.querySelector("svg");

    if (!newPathEl) {
      console.error("No <path> found inside the uploaded SVG.");
      return;
    }

    // Replace path 'd' in-place (keeps binding to pathEl)
    const newD = newPathEl.getAttribute("d");
    if (newD && pathEl) {
      pathEl.setAttribute("d", newD);
    }

    // If the uploaded SVG has a viewBox, copy it to our inline svg so measurements match
    if (newSvgEl && svgEl) {
      const vb = newSvgEl.getAttribute("viewBox");
      if (vb) {
        svgEl.setAttribute("viewBox", vb);
      } else {
        // fallback: copy width/height attributes if viewBox not present
        const w = newSvgEl.getAttribute("width");
        const h = newSvgEl.getAttribute("height");
        if (w && h) {
          svgEl.setAttribute("width", w);
          svgEl.setAttribute("height", h);
        }
      }
    }

    // ensure layout updated before measuring new path start
    requestAnimationFrame(() => {
      // recalc svg bounding, path, etc.
      // setup animation stroke values
      const pathLength = setupPathAnimation(pathEl);
      if (!pathLength) return;

      // determine svgHeight from viewBox (preferred) or fallback to ownerSVGElement height
      const vb = svgEl.viewBox.baseVal;
      const svgHeight =
        vb && vb.height
          ? vb.height
          : svgEl.getBoundingClientRect().height || 9000;

      // set trigger point adaptively (keeps same behavior across widths)
      const updateTrigger = () => {
        triggerPoint = window.innerWidth >= 1445 ? 650 : 900;
      };
      updateTrigger();
      window.addEventListener("resize", updateTrigger);

      // install scroll handler (save for cleanup)
      scrollHandler = installScrollHandler(pathEl, pathLength, svgHeight);
    });
  });

  onDestroy(() => {
    if (typeof window !== "undefined") {
      if (scrollHandler) window.removeEventListener("scroll", scrollHandler);
      window.removeEventListener("resize", () => {});
    }
  });
</script>

<!-- Markup: initial inline svg contains a <=placeholder path. It will be replaced on mount -->
<div class="wrapper" bind:this={wrapperEl}>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    bind:this={svgEl}
    id="Layer_1"
    data-name="Layer 1"
    width="1323.19"
    viewBox="0 0 1323.19 7818.3"
  >
    <!-- initial path (kept so Svelte can bind; content replaced at runtime) -->
    <path
      bind:this={pathEl}
      class="cls-1"
      d="M52.32,0c0,32.34,0,106.48,0,117.43,0,7.92,0,15.84,0,23.76,0,11.82,0,183.77.01,195.58,0,14.59,0,29.18.01,43.76,0,16.23.01,32.45.02,48.68,0,16.74.01,33.47.02,50.21,0,16.12.01,32.23.02,48.35,0,14.33,0,28.65.01,42.98,0,11.5,0,22.99.01,34.49,0,7.47,0,14.95,0,22.42v88.79l67.51,69.26"
    />
  </svg>
</div>

<style>
  .wrapper {
    width: 100%;
    max-width: 1440px;
    margin: 0 auto;
    padding: 100px 0;
    position: absolute;
    top: -400px; /* initial top — script will adjust this value on mount to match old start */
    left: 55%;
    transform: translateX(-50%);
    z-index: -2;
  }

  svg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: auto;
    max-height: 9000px;
    pointer-events: none;
    transition: all 0.6s ease;
  }

  .cls-1 {
    fill: none;
    stroke: #dbd3c3;
    stroke-width: 7px;
    stroke-miterlimit: 20;
    stroke-dasharray: 0;
    stroke-dashoffset: 0;
    transform-origin: center;
  }

  /* hide wrapper on mobile if you used that before */
  @media only screen and (max-width: 800px) {
    .wrapper {
      display: none;
    }
  }
</style>
