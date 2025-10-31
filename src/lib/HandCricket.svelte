<script lang="ts">
  let playerscores = $state([0, 0]);
  let hand1 = $state(-1);
  let hand2 = $state(-1);
  let currPlay = $state(0);
  let winner = $state(0);
  const player = ["Player", "Computer"];
  const declarewin = ["", "Player wins!", "Computer wins...", "Draw!"];

  const hand = ["☝️", "✌️", "👌", "🖖", "👋", "👍", "👉", "🎱", "9️⃣", "🤟"];
  const play = (x: number) => {
    if (winner) return;
    hand1 = x - 1;
    hand2 = Math.floor(Math.random() * 10);
    if (hand1 !== hand2) {
      playerscores[currPlay] =
        currPlay === 0
          ? playerscores[currPlay] + x
          : playerscores[currPlay] + hand2 + 1;
    } else {
      if (currPlay === 0) currPlay = 1;
      else {
        if (playerscores[0] < playerscores[1]) winner = 2;
        else if (playerscores[1] < playerscores[0]) winner = 1;
        else winner = 3;
      }
    }
    if (playerscores[1] > playerscores[0]) winner = 2;
  };
  const reset = () => {
    winner = 0;
    hand1 = -1;
    hand2 = -1;
    currPlay = 0;
    playerscores[0] = 0;
    playerscores[1] = 0;
  };
</script>

<button onclick={() => window.location.reload()}>Back</button>
<div style="display: flex; flex-direction: column;">
  <div id="scoreBoard">
    <div>
      <h2>Player {playerscores[0]}</h2>
    </div>
    <div>
      <h1>{!winner ? player[currPlay] + " is batting" : declarewin[winner]}</h1>
    </div>
    <div>
      <h2>Computer {playerscores[1]}</h2>
    </div>
  </div>
  <div id="playTable">
    <div class="handBtn">{hand[hand1]}</div>
    <div class="handBtn">{hand[hand2]}</div>
  </div>
  <div style="display: flex;">
    <button class="handBtn" onclick={() => play(1)}>☝️</button>
    <button class="handBtn" onclick={() => play(2)}>✌️</button>
    <button class="handBtn" onclick={() => play(3)}>👌</button>
    <button class="handBtn" onclick={() => play(4)}>🖖</button>
    <button class="handBtn" onclick={() => play(5)}>👋</button>
    <button class="handBtn" onclick={() => play(6)}>👍</button>
    <button class="handBtn" onclick={() => play(7)}>👉</button>
    <button class="handBtn" onclick={() => play(8)}>🎱</button>
    <button class="handBtn" onclick={() => play(9)}>9️⃣</button>
    <button class="handBtn" onclick={() => play(10)}>🤟</button>
  </div>
  <button onclick={() => reset()}>Reset</button>
</div>

<style>
  .handBtn {
    height: 100px;
    width: 100px;
    border-radius: 50%;
    background-color: peachpuff;
    font-size: xx-large;
    align-content: center;
    margin-left: 5px;
    margin-right: 5px;
    transition: 0.2s ease all;
    padding: 0;
  }
  .handBtn:hover {
    border-radius: 25%;
    transition: 0.5s ease all;
  }
  #scoreBoard {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 50vw;
    background-color: grey;
    border-radius: 30px;
    padding: 5px;
    box-sizing: content-box;
    align-items: center;
    align-self: center;
    margin-bottom: 10px;
  }
  #playTable {
    width: 40vw;
    padding-left: 20px;
    padding-right: 20px;
    border-radius: 15px;
    height: 150px;
    display: flex;
    justify-content: space-between;
    background-color: brown;
    align-items: center;
    position: static;
    align-self: center;
    margin-bottom: 10px;
  }
</style>
