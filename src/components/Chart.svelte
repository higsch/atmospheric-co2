<script>
  import {
    scaleLinear,
    extent,
    line,
    curveBasis,
    minIndex } from 'd3';

  import Axes from './Axes.svelte';
  import Tooltip from './Tooltip.svelte';

  export let width = 100;
  export let height = 100;
  export let data = [];

  const margin = 20;

  const lineGenerator = line()
    .x(d => d.scaledX)
    .y(d => d.scaledY)
    .curve(curveBasis);

  let hoveredPoint;

  function handleMouseMove(e) {
    if (!xScale) return;
    const hoverDate = xScale.invert(e.clientX);
    const index = minIndex(data.map(d => Math.abs(d.x - hoverDate)));
    hoveredPoint = scaledData[index];
  }

  $: xScale = scaleLinear()
    .domain(extent(data, d => d.x))
    .range([margin, width - margin]);
    
  $: yScale = scaleLinear()
    .domain(extent(data, d => d.y))
    .range([height - margin, margin]);

  $: scaledData = data.map(d => {
    return {
      ...d,
      scaledX: xScale(d.x),
      scaledY: yScale(d.y)
    }
  });
</script>

<svg
  width={width}
  height={height}
  on:mousemove={handleMouseMove}
>
  <Axes
    xScale={xScale}
    yScale={yScale}
  />
  <path
    d={lineGenerator(scaledData)}
  />
  {#each scaledData as point}
    <circle
      cx={point.scaledX}
      cy={point.scaledY}
      r="2"
    />
  {/each}
  <Tooltip
    hoveredPoint={hoveredPoint}
  />
</svg>

<style>
  path {
    fill: none;
    stroke: purple;
    stroke-width: 2px;
  }

  circle {
    fill: white;
    stroke: purple;
  }
</style>