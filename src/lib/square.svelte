<script lang="ts">
  export let value: string = '';
</script>

{#if value}
  <div class="square">
    {value}
  </div>
{:else}
  <button class="square" on:click></button>
{/if}

<style>
  :is(div, button) {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #ffffff;
    color: #000000;
    border: none;
    font-family: inherit;
    font-size: 3rem;
    font-weight: 700;
    cursor: pointer;
  }
</style>
