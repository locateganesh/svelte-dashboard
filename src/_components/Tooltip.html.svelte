<!--
  @component
  Generates a hover tooltip. It creates a slot with an exposed variable via `let:detail` that contains information about the event. Use the slot to populate the body of the tooltip using the exposed variable `detail`.
 -->
 <script>
    /** @type {Object} evt - A svelte event created via [`dispatch`](https://svelte.dev/docs#createEventDispatcher) with event information under `evt.detail.e`. */
    export let evt = {};
  
    /** @type {Number} [offset=-35] - A y-offset from the hover point, in pixels. */
    export let offset = -35;

  </script>
  
  <style>
    .tooltip {
      position: absolute;
      max-width: 300px;
      min-width: 200px;
      font-size: 13px;
      background: rgba(255, 255, 255);
      transform: translate(-50%, -100%);
      padding: 10px 20px;
      z-index: 15;
      border-radius: 5px;
      box-shadow: 0 0 10px 0 rgba(0,0,0,.4);
    }
  </style>
  
  {#if evt.detail}
    <div
      class="tooltip"
      style="
        top:{evt.detail.e.layerY + offset}px;
        left:{evt.detail.e.layerX}px;
      "
    >
      <slot detail={evt.detail}></slot>
    </div>
  {/if}