<script>
  import { getContext } from "svelte";
	import { key } from './config.js';

  const { getMap } = getContext(key);
  const map = getMap();

  export let lat;
  export let lon;

  map.flyTo({
    center: [lat, lon],
    zoom: 9,
    bearing: 0
  });

</script>
