<script>
  import { Route } from "tinro";
  import { Meteor } from "meteor/meteor";
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Moves } from "../api/moves";

  import {
    LoginWindow,
    Logout
  } from "meteor/leveluptutorials:svelte-accounts-ui";

  import AllMoves from "./moves/Moves.svelte";

  let newMove = "";
  let newType = "toprock";

  $: user = useTracker(() => Meteor.userId());

  function handleSubmit(event) {
    Moves.insert({
      title: newMove,
      type: newType,
      userId: $user
    });

    newMove = "";
    newType = "toprock";
  }
</script>

<style>
  :global(:root) {
    --black: #333;
    --red: #e54b4b;
    --lightGrey: #ccc;
    --white: #fff;

    --lineColor: var(--lightGrey);
  }
  header {
    color: var(--white);
    background: var(--black);
  }
</style>

<header>
  <h1>Bboy Tools</h1>
</header>
<!-- 
<nav>
  <a href="/">Home</a>
  <a href="/portfolio">Portfolio</a>
  <a href="/contacts">Contacts</a>
</nav> -->
<!-- 
<Route path="/">
  <h1>It is main page</h1>
</Route> -->

{#if $user}
  <Logout />
{:else}
  <LoginWindow />
{/if}

<main>
  {#if $user}
    <form on:submit|preventDefault={handleSubmit}>
      <input type="text" placeholder="Add new move" bind:value={newMove} />
      <select bind:value={newType}>
        <option value="toprock">Toprock</option>
        <option value="footwork">Footwork</option>
        <option value="freeze">Freeze</option>
        <option value="power">Power</option>
        <option value="burner">Burner</option>
      </select>
      <button>Add Move</button>
    </form>

    <AllMoves user={$user} />
  {/if}

</main>
