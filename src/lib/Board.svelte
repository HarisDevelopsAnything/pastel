<script lang="ts">
  //1 - x, 2 - o, 0 - empty
  let board_state = $state([0, 0, 0, 0, 0, 0, 0, 0, 0]);
  let filled = $state(0);
  let winner = $derived(
    board_state[0] === board_state[1] && board_state[1] === board_state[2]
      ? board_state[0]
      : board_state[3] === board_state[4] && board_state[4] === board_state[5]
        ? board_state[3]
        : board_state[6] === board_state[7] && board_state[7] === board_state[8]
          ? board_state[6]
          : board_state[0] === board_state[3] &&
              board_state[3] === board_state[6]
            ? board_state[0]
            : board_state[1] === board_state[4] &&
                board_state[4] === board_state[7]
              ? board_state[1]
              : board_state[2] === board_state[5] &&
                  board_state[5] === board_state[8]
                ? board_state[2]
                : board_state[0] === board_state[4] &&
                    board_state[4] === board_state[8]
                  ? board_state[0]
                  : board_state[2] === board_state[4] &&
                      board_state[4] === board_state[6]
                    ? board_state[2]
                    : 0
  );
  let draw = $derived(filled === 9 && !winner);
  const place = ["", "X", "O", "G", "A", "M", "E", "O", "V", "E", "R", "!"];
  let currPlay = $state(1);
  const makeMove = (x: number) => {
    if (winner) return;
    if (board_state[x] === 0) {
      board_state[x] = currPlay;
      currPlay = currPlay === 1 ? 2 : 1;
      filled++;
    }
    if (winner) {
      document.getElementById("board").style = "background-color: lime;";
    }
    if (draw) {
      document.getElementById("board").style = "background-color: grey;";
    }
  };
  const resetBoard = () => {
    let i = 0;
    const fancyClear = setInterval(() => {
      board_state[i] = i + 3;
      i++;
      console.log(i);
      if (i == 10) {
        clearInterval(fancyClear);
        for (let i = 0; i < 9; i++) board_state[i] = 0;
        currPlay = 1;
        draw = false;
        filled = 0;
        document.getElementById("board").style =
          "background-color: antiquewhite;";
      }
    }, 159.7232);
  };
</script>

<button onclick={() => window.location.reload()}>Back</button>
<h1>
  {!draw && winner === 0
    ? place[currPlay] + "'s move!"
    : draw
      ? "Draw!"
      : "Winner:" + place[winner]}
</h1>
<div id="board">
  <div style="display: flex; width: 100%; height: 100px;">
    <button class="tic" onclick={() => makeMove(0)}
      >{place[board_state[0]]}</button
    >
    <button class="tic" onclick={() => makeMove(1)}
      >{place[board_state[1]]}</button
    >
    <button class="tic" onclick={() => makeMove(2)}
      >{place[board_state[2]]}</button
    >
  </div>
  <div style="display: flex; width: 100%; height: 100px;">
    <button class="tic" onclick={() => makeMove(3)}
      >{place[board_state[3]]}</button
    >
    <button class="tic" onclick={() => makeMove(4)}
      >{place[board_state[4]]}</button
    >
    <button class="tic" onclick={() => makeMove(5)}
      >{place[board_state[5]]}</button
    >
  </div>
  <div style="display: flex; width: 100%; height: 100px;">
    <button class="tic" onclick={() => makeMove(6)}
      >{place[board_state[6]]}</button
    >
    <button class="tic" onclick={() => makeMove(7)}
      >{place[board_state[7]]}</button
    >
    <button class="tic" onclick={() => makeMove(8)}
      >{place[board_state[8]]}</button
    >
  </div>
</div>
<button onclick={() => resetBoard()}>Reset</button>

<style>
  #board {
    width: 300px;
    height: 300px;
    background-color: antiquewhite;
    border-radius: 30px;
  }
  .tic {
    width: 90px;
    height: 90px;
    margin: 5px;
    border-radius: 30px;
    transition: 0.5s ease all;
    font-size: x-large;
  }
  .tic:hover {
    border-radius: 50px;
    transition: 0.5s ease all;
  }
</style>
