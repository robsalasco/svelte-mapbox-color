<script>
  import mapboxgl from "mapbox-gl";
  import { onMount, setContext } from "svelte";
  import { mapBoxKey } from "./config.js";

  const lightStyle = "mapbox://styles/robsalasco/ckphuacg002mz18pkga2rktq2?optimize=true";

  let map;
  export let roadcolor;

  onMount(() => {
    mapboxgl.accessToken = mapBoxKey;
    map = new mapboxgl.Map({
      container: "map",
      style: lightStyle,
      zoom: 14,
      center: [-70.648956, -33.450349],
    });

    map.on("load", function () {
      map.setPaintProperty('road-primary','line-color', roadcolor)
      map.setPaintProperty('road-street','line-color', roadcolor)
      map.setPaintProperty('road-street-low','line-color', roadcolor)
      map.setPaintProperty('road-minor','line-color', roadcolor)
      map.setPaintProperty('road-minor-low','line-color', roadcolor)
      map.setPaintProperty('road-secondary-tertiary','line-color', roadcolor)
      map.setPaintProperty('road-major-link','line-color', roadcolor)

    });
  });

  setContext("mapBoxKey", {
    getMap: () => map,
  });
</script>

<svelte:head>
  <link
    href="https://api.mapbox.com/mapbox-gl-js/v1.0.0/mapbox-gl.css"
    rel="stylesheet"
  />
</svelte:head>

<div id="map" />

<style>
  #map {
    height: 700px;
  }
</style>
