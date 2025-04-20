<script lang="ts">
    import { recieve } from "./transitions.js";
    let { founded }: { founded: string[] } = $props();
</script>

<div class="found">
    {#each founded as emoji (emoji)}
        <div class="pair">
            <span in:recieve={{key: `${emoji}a`}}>{emoji}</span>
            <span in:recieve={{key: `${emoji}b`}}>{emoji}</span>
        </div>
    {/each}
</div>

<style>
    .found {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: .5em;
        height: 100%;
        filter: drop-shadow(0 0 .5em #000);
    }

    .pair {
        width: 4em;
        height: 4em;
        border-radius: 50%;
        background-color: #fff;
    }
    span {
        position: absolute;
        font-size: 2.8em;
    }
</style>