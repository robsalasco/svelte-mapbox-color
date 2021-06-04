<script>
  import { onMount, setContext } from "svelte";
	import { mapboxgl, key } from './config.js';

  const lightStyle = "mapbox://styles/robsalasco/ckphuacg002mz18pkga2rktq2?optimize=true";

  let map;

  setContext(key, {
    getMap: () => map,
  });
  
  onMount(() => {
    map = new mapboxgl.Map({
      container: 'map',
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

<div id="map">
	{#if map}
		<slot></slot>
	{/if}
</div>

<style>
  #map {
    height: 700px;
  }
</style>
