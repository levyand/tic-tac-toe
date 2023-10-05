<script lang="ts">
  const win_conditions = [
    [0,1,2],
    [3,4,5],
    [6,7,8],
    [0,3,6],
    [1,4,7],
    [2,5,8],
    [0,4,8],
    [2,4,6]
  ];
  let winner: 'X' | 'O' | undefined = undefined;

  let squares = Array<string>(9);
  let player: 'X' | 'O' = 'X';

  const handle_click = (index: number) => () => {
    squares[index] = player;

    // check win conditions
    const player_squares: number[] = [];
    squares.forEach((val, index) => {
      if (val === player) player_squares.push(index);
    });

    const win = win_conditions.some(opt => opt.every(index => player_squares.includes(index)));
    if (win) {
      winner = player;
      return;
    }
    // win_conditions.forEach(opt => {
    //   const win = opt.every(index => player_squares.includes(index));

    //   if (win) {
    //     winner = player;
    //     return;
    //   }
    // });

    player = player === 'X' ? 'O' : 'X';
  };

  function reset() {
    squares = Array<string>(9);
    player = 'X';
    winner = undefined;
  }
</script>

<h3>Current Player: {player}</h3>

<div>
  <button on:click={reset}>
    Reset
  </button>
</div>

<div class="board">
  {#each squares as s, index}
    {#if s}
      <div class="square">
        {s}
      </div>
    {:else}
      <button class="square" on:click={handle_click(index)}>&nbsp;</button>
    {/if}
  {/each}
</div>

{#if winner}
  <h2>Player {winner} Wins!</h2>
{/if}

<style>
  .board {
    display: grid;
    gap: 8px;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    width:fit-content;
    margin-inline: auto;
    background-color: #000000;
  }

  .square {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #ffffff;
    color: #000000;
    border: none;
    font-family: inherit;
    font-size: 3rem;
    font-weight: 700;
  }
</style>
