<script>
  import { onMount } from 'svelte';
  import { csv } from 'd3';

  import Chart from './components/Chart.svelte';

  let data = [];
  let width, height;

  onMount(async () => {
    const rawData = await csv('data/in_situ_co2.csv', d => {
      return {
        x: +d.Date,
        y: +d.CO2
      };
    });

    data = rawData.filter(d => d.y > 0);
  });
</script>

<main
  bind:clientWidth={width}
  bind:clientHeight={height}
>
  <Chart
    width={width}
    height={height}
    data={data}
  />
</main>

<style>
  main {
    width: 100%;
    height: 100%;
    overflow: hidden;
  }
</style>