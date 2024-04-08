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
    export let getLabelName;
  
    /** @type {Function} [formatLabelName=d => d] - An optional formatting function. */
    export let formatLabelName = d => d;

    // console.log("labels", labels, data);

  </script>
  <g class="labels">
    {#each labels as d}
      <text
        class="label"
        x={$xGet(d)}
        y={$yGet(d)}
      >{formatLabelName(getLabelName(d))}</text>
    {/each}
  </g>
  
  <style>
    .labels {
      pointer-events: none;
    }
    .label {
      position: absolute;
      font-size: 12px;
      text-anchor: middle;
    }
  </style>