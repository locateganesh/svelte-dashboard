<!--
  @component
  Generates an SVG stacked bar chart and sets the color via an ordinal scale in `zScale`.
 -->
<script>
  import { getContext } from 'svelte';

  const { data, xGet, yGet, zGet, yScale } = getContext('LayerCake');

  /** @type {Number} [separator] - Separator between bars */
  export let separator = false;

  $: columnWidth = d => {
    const xVals = $xGet(d);
		return xVals[1] - xVals[0];
  };

  // console.log("separator", separator);
</script>

<g class="bar-group">
  {#each $data as series}
    {#each series as d, i}
      <rect
        class='group-rect'
        data-id="{i}"
        x="{$xGet(d)[0]}"
        y="{$yGet(d)}"
        height={$yScale.bandwidth() / 2}
        width="{columnWidth(d)}"
        fill={$zGet(series)}
      >
      <text>ahhd</text>
    </rect>
      {#if separator}
        <!-- <line x1={columnWidth(d) / 2 } y1="50" x2={columnWidth(d)} y2="50" stroke="#aeaeae" stroke-width="1" /> -->
      {/if}
    {/each}
  {/each}
</g>
