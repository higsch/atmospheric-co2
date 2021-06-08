<script>
  export let hoveredPoint;
</script>

{#if (hoveredPoint)}
  <g
    class="tooltip"
    transform="translate({hoveredPoint.scaledX} {hoveredPoint.scaledY})"
  >
    <circle
      cx="0"
      cy="0"
      r="5"
    />
    <g transform="translate(10 5)">
      <text class="background">
        {hoveredPoint.y} ppm
      </text>
      <text>
        {hoveredPoint.y} ppm
      </text>
    </g>
  </g>
{/if}

<style>
  circle {
    fill: none;
    stroke: black;
    stroke-width: 2;
  }

  text {
    font-family: 'Courier New', Courier, monospace;
  }

  text.background {
    fill: white;
    stroke: white;
    stroke-width: 5;
  }
</style>