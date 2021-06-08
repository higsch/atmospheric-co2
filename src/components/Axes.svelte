<script>
  export let xScale;
  export let yScale;

  $: xTicks = xScale.ticks();
  $: yTicks = yScale.ticks();
</script>

<g class="axes">
  <g
    class="x-axis"
    transform="translate(0 {yScale.range()[0]})"
  >
    {#each xTicks as tick}
      <g
        class="tick"
        transform="translate({xScale(tick)} 0)"
      >
        <circle
          cx="0"
          cy="0"
          r="3"
        />
        <text
          x="10"
          y="5"
        > 
          {tick}
        </text>
      </g>
    {/each}
  </g>
  <g
    class="y-axis"
    transform="translate({xScale.range()[0]} 0)"
  >
    {#each yTicks as tick, i}
      <g
        class="tick"
        transform="translate(0 {yScale(tick)})"
      >
        <circle
          cx="0"
          cy="0"
          r="3"
        />
        <text
          x="10"
          y="5"
        >
          {tick}
          {#if (i === yTicks.length - 1)}
            ppm
          {/if}
        </text>
      </g>
    {/each}
  </g>
</g>

<style>
  circle {
    stroke: none;
    fill: black;
  }

  text {
    font-family: 'Courier New', Courier, monospace;
  }
</style>