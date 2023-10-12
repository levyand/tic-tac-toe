<script lang="ts">
  import GameBoard from './game-board.svelte';
  
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

  function handle_selection(index: number) {
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
    
    player = player === 'X' ? 'O' : 'X';
  }

  function reset() {
    squares = Array<string>(9);
    player = 'X';
    winner = undefined;
  }
</script>

<main>
  <h1>Tic Tac Toe</h1>
  
  <h3>Current Player: {player}</h3>

  <div>
    <button on:click={reset}>
      Reset
    </button>
  </div>

  <GameBoard
    {squares}
    on:select={e => handle_selection(e.detail.index)}
  />
  
  {#if winner}
    <h2>Player {winner} Wins!</h2>
  {/if}
</main>

<style>
  main {
    width: fit-content;
    margin-inline: auto;
  }
</style>
