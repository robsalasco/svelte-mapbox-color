<script>
  import Mapbox from "./Mapbox.svelte";
  import Layout from './Layout.svelte';
  import {HsvPicker} from 'svelte-color-picker';

  let selected = "#bd0026";
  let mounted = true;


  $: { reMountMap( selected ) }
    function reMountMap(){
      mounted = false;
      setTimeout(() => mounted = true, 0);
    }

  function colorCallback(rgb) {
    let r = rgb.detail.r;
		let g = rgb.detail.g;
		let b = rgb.detail.b;
    selected = `rgb(${r},${g},${b})`;
  }

</script>

<Layout>
  <span slot="left">
  <HsvPicker on:colorChange={colorCallback} startColor={selected}/>
  </span>
  <span slot="right">
    {#if mounted}
      <Mapbox roadcolor={selected}/>
    {/if}
  </span>
</Layout>
