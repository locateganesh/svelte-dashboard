
<script>
    export let title = ''
    export let text = ''
</script>
<div class="flex chartHeader">
    <div class="pr-[30px]">
        <h3 class="font-bold text-[18px]">{title || 'Untitled'}</h3>
        {#if text.length}
            <p class="text-[14px] mt-[5px] leading-[1.3]">{text}</p>
        {/if}
    </div>
    <div>
        <button class="bookmark"><img class="w-[15px]" src="/bookmark.png" alt="bookmark" /></button>
    </div>
</div>

<style lang="scss">
    .chartHeader {
        .bookmark {
            width: 36px;
            height: 36px;
            background-color: #d9e0f1;
            border-radius: 5px;
            text-align: center;
            img {
                margin: auto;
            }
        }
    }
</style>