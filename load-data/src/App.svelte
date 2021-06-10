<script>
  import { onMount } from 'svelte';
  import { csv } from 'd3';

  let data = [];

  onMount(async () => {
    const rawData = await csv('data/in_situ_co2.csv', d => {
      return {
        x: +d.Date,
        y: +d.CO2
      };
    });

    data = rawData.filter(d => d.y > 0);

    console.log(data);
  });
</script>