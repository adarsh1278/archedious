<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { MotionPathPlugin } from "gsap/MotionPathPlugin";

    gsap.registerPlugin(ScrollTrigger, MotionPathPlugin);

    export let svgPath = "/last.svg";
    export let className = "";
    export let showPen = true;

    let container;
    let penFollower;

    onMount(() => {
        fetch(svgPath)
            .then((response) => response.text())
            .then((svgText) => {
                container.innerHTML = svgText;
                const svg = container.querySelector("svg");
                
                if (svg) {
                    if (className) svg.classList.add(className);
                    svg.style.position = "relative";
                    
                    const paths = Array.from(svg.querySelectorAll("path"));
                    
                    if (paths.length === 0) return;
                    
                    // Prepare all paths
                    paths.forEach((path) => {
                        const length = path.getTotalLength();
                        const originalFill = path.getAttribute("fill") || "#989086";
                        
                        path.style.strokeDasharray = length;
                        path.style.strokeDashoffset = length;
                        path.style.stroke = originalFill;
                        path.style.strokeWidth = "2";
                        path.style.strokeLinecap = "round";
                        path.style.strokeLinejoin = "round";
                        path.style.fill = originalFill;
                        path.style.fillOpacity = "0";
                    });
                    
                    // Create master timeline
                    const timeline = gsap.timeline({
                        scrollTrigger: {
                            trigger: container,
                            start: "top 80%",
                            end: "bottom 20%",
                            scrub: 1,
                            invalidateOnRefresh: true
                        }
                    });
                    
                    // Add each path animation sequentially
                    paths.forEach((path, index) => {
                        const length = path.getTotalLength();
                        
                        // Animate stroke drawing (slower)
                        timeline.to(path, {
                            strokeDashoffset: 0,
                            duration: length / 1500,
                            ease: "none"
                        }, index === 0 ? 0 : ">");
                        
                        // Animate pen follower along this path
                        if (showPen && penFollower) {
                            timeline.to(penFollower, {
                                motionPath: {
                                    path: path,
                                    align: path,
                                    alignOrigin: [0.5, 0.5],
                                    autoRotate: false
                                },
                                duration: length / 1500,
                                ease: "none"
                            }, "<");
                        }
                    });
                    
                    // Fill all paths earlier - starts before drawing completes
                    timeline.to(paths, {
                        fillOpacity: 1,
                        duration: 0.4,
                        ease: "power2.inOut",
                        stagger: 0
                    }, "-=2.4");
                    
                    // Hide pen after fill starts
                    if (showPen && penFollower) {
                        timeline.to(penFollower, {
                            opacity: 0,
                            duration: 0.01
                        }, ">");
                    }
                }
            });
    });
</script>

<div bind:this={container} class="svg-line-drawing">
    {#if showPen}
        <div bind:this={penFollower} class="pen-follower"></div>
    {/if}
</div>

<style>
    .svg-line-drawing {
        display: inline-block;
        position: relative;
    }
    
    .pen-follower {
        position: absolute;
        width: 12px;
        height: 12px;
        background: #989086;
        border-radius: 50%;
        pointer-events: none;
        z-index: 10;
        box-shadow: 0 0 8px rgba(152, 144, 134, 0.6);
        transform: translate(-50%, -50%);
    }
</style>
