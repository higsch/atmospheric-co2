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

  $: xScale = scaleLinear()
    .domain(extent(data, d => d.x))
    .range([margin, width - margin]);
    
  $: yScale = scaleLinear()
    .domain(extent(data, d => d.y))
    .range([height - margin, margin]);

  $: lineGenerator = line()
    .x(d => xScale(d.x))
    .y(d => yScale(d.y))
    .curve(curveBasis);
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
    d={lineGenerator(data)}
  />
  {#each data as point}
    <circle
      cx={xScale(point.x)}
      cy={yScale(point.y)}
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