<script lang="ts">
    import Game from "./Game.svelte";
    import '../styles.css';
	import Modal from "./Modal.svelte";

    let state: 'waiting' | 'playing' | 'paused' | 'won' | 'lost' = $state('playing');
</script>

<Game />

{#if state !== 'playing'}
    <Modal>
        {#if state === 'waiting'}
            <h1>Please select the level of game</h1>
        {/if}
    </Modal>
{/if}