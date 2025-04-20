<script lang="ts">
	import { onMount } from "svelte";
	import Countdown from "./Countdown.svelte";
	import Found from "./Found.svelte";
	import Grid from "./Grid.svelte";
    import { levels } from "./levels.js";
    import type { Level } from "./levels.js";
	import { shuffle } from "./utils.js";

    const level = levels[0];
    const size: number = level.size;

    let grid: string[] = createGrid(level);
    let founded: string[] = [];
    let remaining: number = level.duration;
    let duration: number = level.duration;
    let playing: boolean = true;

    function createGrid(level: Level): string[] {
        const copy = level.emojis.slice();
        const pairs: string[] = [];

        for(let i = 0; i < (level.size * level.size) / 2; i++) {
            const index = Math.floor(Math.random() * copy.length);
            const emojis = copy[index];

            copy.slice(index, 1);
            pairs.push(emojis);
        }

        pairs.push(...pairs);

        return shuffle(pairs);
    }

    function found(event: string, data: {emoji: string}) {
        if(event === 'found') {
            founded = [...founded, data.emoji];
        }
    }

    function countDown() {
        const start = Date.now();
        let remainingAtStart = remaining;

        function loop()  {
            if(!playing) return;
            requestAnimationFrame(loop);

            remaining = remainingAtStart - (Date.now() - start);

            if(remaining <= 0) {
                // TODO: Game over
                playing = false;
            }
        }

        loop();
    }

    onMount(countDown);
</script>

<div class="game">
    <div class="info">
        <Countdown 
            {remaining} 
            {duration} 
            onclick={() => {
                // todo
            }} 
        />
    </div>
    <div class="grid-container">
        <Grid {grid} {founded} {found} />
    </div>
    <div class="info">
        <Found {founded} />
    </div>
</div>

<style>
    .game {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        font-size: min(1vmin, 0.5em);
    }

    .info {
        width: 80em;
        height: 10em;
    }

    .grid-container {
        width: 80em;
        height: 80em;
    }
</style>