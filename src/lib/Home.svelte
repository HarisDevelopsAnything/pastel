<script lang="ts">
  import Board from "./Board.svelte";
  import HandCricket from "./HandCricket.svelte";
  let currPage = $state(0);
</script>

<main>
  {#if currPage === 0}
    <div>
      <h1>Pastel</h1>
      <div>
        <button onclick={() => (currPage = 1)}>TicTacToe</button>
        <button onclick={() => (currPage = 2)}>Hand Cricket</button>
      </div>
    </div>
  {:else if currPage === 1}
    <Board />
  {:else}
    <HandCricket />
  {/if}
</main>
