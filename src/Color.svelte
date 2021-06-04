<script>
  import { getContext } from "svelte";
	import { key } from './config.js';


  const { getMap } = getContext(key);
  const map = getMap();

  export let roadcolor;

  map.on("idle", function () {
      map.setPaintProperty('road-primary','line-color', roadcolor)
      map.setPaintProperty('road-street','line-color', roadcolor)
      map.setPaintProperty('road-street-low','line-color', roadcolor)
      map.setPaintProperty('road-minor','line-color', roadcolor)
      map.setPaintProperty('road-minor-low','line-color', roadcolor)
      map.setPaintProperty('road-secondary-tertiary','line-color', roadcolor)
      map.setPaintProperty('road-major-link','line-color', roadcolor)

    });
    


</script>

