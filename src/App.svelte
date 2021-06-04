<script>
  import Mapbox from "./Mapbox.svelte";
  import Color from "./Color.svelte";
  import Layout from './Layout.svelte';
  import {HsvPicker} from 'svelte-color-picker';

  let selected = "#bd0026";
  let mounted = true;

  function colorCallback(rgb) {
    let r = rgb.detail.r;
		let g = rgb.detail.g;
		let b = rgb.detail.b;
    selected = `rgb(${r},${g},${b})`;
  }

  $: { reMountMap( selected ) }
    function reMountMap(){
      mounted = false;
      setTimeout(() => mounted = true, 0);
    }

</script>

<Layout>
  <span slot="left">
  <HsvPicker on:colorChange={colorCallback} startColor={selected}/>
  {selected}
  </span>
  <span slot="right">
      <Mapbox>
        {#if mounted}

        <Color roadcolor={selected} />
            {/if}
      </Mapbox>
      

  </span>
</Layout>
