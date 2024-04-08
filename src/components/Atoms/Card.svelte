<script>
    export let customClass = ''
</script>

<div class={`card bg-white border rounded-xl ${customClass}`}>
    <slot />
</div>

<style lang="scss">
    .card {
        position: relative;
        min-height: 100px;
        width: 100%;
        height: 100%;
        padding: 20px 15px;
        box-shadow:0 0 5px 1px rgba(0,0,0,.15);
        &.charts {
            padding: 35px;
        }
    }
</style>
