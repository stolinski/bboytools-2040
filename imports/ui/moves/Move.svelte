<script>
  export let move;
  import { fade } from "svelte/transition";

  import { Close } from "/imports/ui/elements";
  import { Moves } from "../../api/moves";
  let updateRes = move.title;

  function deleteRes() {
    Moves.remove(move._id);
  }

  function handleSubmit(event) {
    Moves.update(
      {
        _id: move._id
      },
      {
        title: updateRes
      }
    );
  }
</script>

<style>
  li {
    padding: 20px;
    border-bottom: solid 1px var(--lineColor);
  }
  li > * {
    margin: 0;
  }
</style>

<li transition:fade>
  <div class="move-card">
    <p>{move.title}</p>
    <Close on:click={deleteRes} />
  </div>
</li>
