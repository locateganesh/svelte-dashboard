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

    const reversedForBar = 10; 
    const leftModified = (getD, numb) => {
      const offset = 35;
       if (numb < reversedForBar) {
         return getD + 30;
       } else {
         return getD - 50;
       }
    }

  </script>
  
  {#each labels as d} 
    <div
      data-id={$xGet(d)}
      class={`label${getLabelName(d) < reversedForBar ? ' label-smaller' : ''}`}
      style="
        top:{$yGet(d) + 9}px;
        left:{leftModified($xGet(d), getLabelName(d))}px;
      "
    >{formatLabelName(getLabelName(d))}</div>
  {/each}
  
  <style lang="scss">
    .label {
      position: absolute;
      // transform: translate(-50%, -50%);
      font-size: 16px;
      color:#fff;
      &-smaller {
        color:#000;
      }
    }
  </style>