<script lang="ts">
	import { send } from "./transitions.js";

    let { 
      emoji, 
      onclick, 
      selected, 
      founded, 
      group 
    }: { emoji: string, onclick: () => void, selected: boolean, founded: boolean, group: 'a' | 'b' } = $props();
</script>

<div class="square" class:flipped={selected || founded}>
    <button {onclick} aria-label="Click to flip"></button>

    <div class="background"></div>

    {#if !founded}
        <span out:send={{ key: `${emoji}${group}` }}>{emoji}</span>
    {/if}
</div>


<style>
    .square {
        display: flex;
        justify-content: center;
        align-items: center;
        transform-style: preserve-3d;
        transition: transform .4s;
        position: relative;
    }

    .background {
        background-color: white;
        border: 0.2em solid #ccc;
        border-radius: 1em;
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        transform: rotateY(180deg);
    }

    span {
        font-size: 5em;
        pointer-events: none;
        transform: rotateY(180deg);
        backface-visibility: hidden;
    }

    .flipped {
        transform: rotateY(180deg);
    }

    button {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        background-color: #ccc;
        border: none;
        border-radius: 1em;
        font-size: inherit;
    }
</style>