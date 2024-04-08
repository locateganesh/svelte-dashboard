<!--
  @component
  Generates an SVG bar chart.
 -->
<script>
  import { getContext, createEventDispatcher } from 'svelte';

  const { data, xGet, yGet, xScale, yScale } = getContext('LayerCake');

  /** @type {String} [fill='#00bbff'] - The shape's fill color. This is technically optional because it comes with a default value but you'll likely want to replace it with your own color. */
  export let fill = '#00bbff';
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

  // console.log("Bar Data ", $data);
</script>

<g 
  class="bar-group"
  on:mouseout={() => dispatch("mouseout")}
  on:blur={() => dispatch("mouseout")}
  role="button"
  tabindex="0"
  >
  {#each $data as d, i}
    <!-- <rect
      class='group-rect'
      data-id="{i}"
      x="{$xScale.range()[0]}"
      y="{$yGet(d)}"
      height={$yScale.bandwidth()}
      width="{$xGet(d)}"
      {fill}
    ></rect> -->
    <!-- <path
      class='group-rect'
      data-id={i}
      d={`M${$xScale.range()[0]},${$yGet(d)}h${$xGet(d)}c5.5,0,10,4.5,10,10v${$yScale.bandwidth()}c0,5.5-4.5,10-10,10H0V0z`}
      fill={fill}
    ></path> -->
    <path
      class='group-rect'
      data-id="{i}"
      d="M {$xScale.range()[0]},{$yGet(d)} h {$xGet(d)} a 10,10 0 0 1 10,10 v {$yScale.bandwidth() - 10} a 10,10 0 0 1 -10,10 h -{$xGet(d)} Z"
      {fill}
      on:mouseover={(e) => dispatch("mousemove", { e, props: d })}
      on:focus={(e) => dispatch("mousemove", { e, props: d })}
      on:mousemove={(e) => handleMousemove(e, d)}
      role="button"
      tabindex="0"
    ></path>
  {/each}
</g>

<style>
  path:focus {
    outline: none;
  }
</style>