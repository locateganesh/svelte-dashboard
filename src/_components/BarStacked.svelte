<!--
  @component
  Generates an SVG stacked bar chart and sets the color via an ordinal scale in `zScale`.
 -->
<script>
  import { getContext, createEventDispatcher } from 'svelte';

  const { data, xGet, yGet, zGet, yScale } = getContext('LayerCake');

  /** @type {Number} [separator] - Separator between bars */
  export let separator = false;

  $: columnWidth = d => {
    const xVals = $xGet(d);
		return xVals[1] - xVals[0];
  };

  const dispatch = createEventDispatcher();
  function handleMousemove() {
    return function handleMousemoveFn(e) {
      raise(this);
      // When the element gets raised, it flashes 0,0 for a second so skip that
      if (e.layerX !== 0 && e.layerY !== 0) {
        dispatch("mousemove", { e });
      }
    };
  }

  // console.log("$data", $data);
</script>

<g 
  class="bar-group"
  on:mouseout={() => dispatch("mouseout")}
  on:blur={() => dispatch("mouseout")}
  >
  {#each $data as series}
    {#each series as d, i}
      <rect
        class='group-rect'
        data-id="{i}"
        data-d={d}
        x="{$xGet(d)[0]}"
        y="{$yGet(d)}"
        height={$yScale.bandwidth() / 2}
        width="{columnWidth(d)}"
        fill={$zGet(series)}
        on:mouseover={(e) => dispatch("mousemove", { e, props: d })}
        on:focus={(e) => dispatch("mousemove", { e, props: d })}
        on:mousemove={(e) => handleMousemove(e, d)}
      >
    </rect>
      {#if separator}
        <!-- <line x1={columnWidth(d) / 2 } y1="50" x2={columnWidth(d)} y2="50" stroke="#aeaeae" stroke-width="1" /> -->
      {/if}
    {/each}
  {/each}
</g>
