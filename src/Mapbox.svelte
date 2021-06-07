<script>
  import { onMount, setContext } from "svelte";
	import { mapboxgl, key } from './config.js';

  const lightStyle = "mapbox://styles/robsalasco/ckphuacg002mz18pkga2rktq2?optimize=true";

  export let map = null

  setContext(key, {
    getMap: () => map,
  });
  
  let container;

  export function flyTo () {
    map.flyTo({
    center: [75, 75],
    zoom: 9,
    bearing: 0
  });
  }

  onMount(() => {
    map = new mapboxgl.Map({
      container: container,
      style: lightStyle,
      zoom: 14,
      center: [-70.648956, -33.450349],
    });

  });

</script>

<svelte:head>
  <link
    href="https://api.mapbox.com/mapbox-gl-js/v1.0.0/mapbox-gl.css"
    rel="stylesheet"
  />
</svelte:head>

<div bind:this={container}>
	{#if map}
		<slot></slot>
	{/if}
</div>

<style>
  div {
    height: 700px;
  }
</style>