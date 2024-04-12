<!--
  @component
  Adds HTML text labels based on a given list.
 -->
 <script>
    import { getContext } from 'svelte';
  
    const { xGet, yGet } = getContext('LayerCake');
  
    /** @type {Array} labels - An array of objects that contain a field containing text label and data fields. */
    export let labels;
  
    /** @type {Function} getLabelName= - An accessor function to return the label field on your objects in the `labels` array. */
    //export let getLabelName;
  
    /** @type {Function} [formatLabelName=d => d] - An optional formatting function. */
    //export let formatLabelName = d => d;

    // console.log("labels", labels, data);
    // console.log("stackedLabels", labels[0].key);

    const calcValue = (n1, n0) => {
      if (n1 !== null && n0 !== null) {
        return (+n1) - (+n0);
      }
    };

  </script>
  <!-- x={$xGet(d) + $xGet.bandwidth() / 2}
          y={$yGet(d[1]) - 10} -->
  <g class="labels">
    {#each labels as stack (stack.key)}
      {#each stack as d (d.data.countries)}
        <text
          class="label myCustomLabel"
          data-x={calcValue(d[1], d[0])}
          x={$xGet(d)[1] - (calcValue(d[1], d[0]) < 10 ? 27 : 36)}
          y={$yGet(d) + 17}
        >
          {calcValue(d[1], d[0]) > 7 ? Math.round(calcValue(d[1], d[0])).toString() + '%' : ''} 
        </text>
      {/each}
    {/each}
  </g>
  
  <style>
    .label {
      font-size: 12px;
      fill: #fff;
      pointer-events: none;
    }
  </style>
