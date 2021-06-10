<script>
  import {
    scaleLinear,
    extent } from 'd3';

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

  $: scaledData = data.map(d => {
    return {
      ...d,
      scaledX: xScale(d.x),
      scaledY: yScale(d.y)
    }
  });

  $: console.log(scaledData);
</script>

<svg
  width={width}
  height={height}
>
</svg>

<style>
  svg {
    box-sizing: border-box;
    border: 5px solid cyan;
    background-color: purple;
  }
</style>