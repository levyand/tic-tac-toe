<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import Square from './square.svelte';

  const dispatch = createEventDispatcher<{ select: { index: number } }>();

  export let squares: string[];

  function handle_click(index: number) {
    dispatch('select', {
      index
    });
  }
</script>

<div>
  {#each squares as s, index}
    <Square value={s} on:click={() => handle_click(index)} />
  {/each}
</div>

<style>
  div {
    display: grid;
    gap: 8px;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    background-color: #000000;
  }
</style>
