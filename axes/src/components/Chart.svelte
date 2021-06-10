<script>
  import {
    scaleLinear,
    extent,
    line,
    curveBasis } from 'd3';

  import Axes from './Axes.svelte';

  export let width = 100;
  export let height = 100;
  export let data = [];

  const margin = 20;

  const lineGenerator = line()
    .x(d => d.scaledX)
    .y(d => d.scaledY)
    .curve(curveBasis);

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