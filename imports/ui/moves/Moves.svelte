<script>
  import { Meteor } from "meteor/meteor";
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Moves } from "../../api/moves";

  import Move from "./Move.svelte";
  export let user;

  let toprock = [];
  let footwork = [];
  let power = [];
  let freeze = [];
  let burner = [];
  let goDown = [];

  $: moves = Moves.find({
    userId: user
  });

  $: if ($moves) {
    toprock = $moves.filter(item => item.type === "toprock");
    footwork = $moves.filter(item => item.type === "footwork");
    power = $moves.filter(item => item.type === "power");
    freeze = $moves.filter(item => item.type === "freeze");
    burner = $moves.filter(item => item.type === "burner");
    goDown = $moves.filter(item => item.type === "goDown");
  }

  // moves.filter(item => item.type === "toprock");
</script>

<style>
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .moves {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 20px;
  }
</style>

<div class="moves">
  <div>
    <h3>Toprock</h3>
    <ul>
      {#each toprock as move}
        <Move {move} />
      {/each}
    </ul>
  </div>
  <div>
    <h3>Footwork</h3>
    <ul>
      {#each footwork as move}
        <Move {move} />
      {/each}
    </ul>
  </div>
  <div>
    <h3>Freeze</h3>
    <ul>
      {#each freeze as move}
        <Move {move} />
      {/each}
    </ul>
  </div>
  <div>
    <h3>Power</h3>
    <ul>
      {#each power as move}
        <Move {move} />
      {/each}
    </ul>
  </div>

  <div>
    <h3>Go Down</h3>
    <ul>
      {#each goDown as move}
        <Move {move} />
      {/each}
    </ul>
  </div>
  <div>
    <h3>Burner</h3>
    <ul>
      {#each burner as move}
        <Move {move} />
      {/each}
    </ul>
  </div>
</div>
