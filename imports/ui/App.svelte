<script>
  import Route from "tinro/cmp/Route.svelte";
  import { router } from "tinro/cmp/index.js";
  import { Meteor } from "meteor/meteor";
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Moves } from "../api/moves";
  import Nav from "./elements/Nav.svelte";
  import BattleMode from "./battle/BattleMode";

  import { LoginWindow, Logout } from "meteor/levelup:svelte-accounts-ui";

  import AllMoves from "./moves/Moves.svelte";

  let newMove = "";
  let newType = "toprock";

  $: user = useTracker(() => Meteor.userId());

  $: if ($user) {
    router.goto("/moves");
  }

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
  header {
    color: var(--white);
    background: var(--black);
    height: 2rem;
    display: flex;
    box-shadow: var(--level1);
    padding: 0 2.5%;
    margin-block-end: 2rem;
  }
  main {
    margin: 0 auto;
    width: 95%;
  }
</style>

<header>
  <h1>Bboy Tools</h1>
  {#if $user}
    <Logout />
  {/if}
</header>

<Nav />

<Route path="/">
  <div>

    <div class="card card-login">
      <LoginWindow />
    </div>
  </div>
</Route>

<Route path="/battle">
  <BattleMode />
</Route>

<Route path="/moves">
  <main>
    {#if $user}
      <form on:submit|preventDefault={handleSubmit}>
        <input type="text" placeholder="Add new move" bind:value={newMove} />
        <select bind:value={newType}>
          <option value="toprock">Toprock</option>
          <option value="footwork">Footwork</option>
          <option value="freeze">Freeze</option>
          <option value="power">Power</option>
          <option value="goDown">Go Down</option>
          <option value="burner">Burner</option>
        </select>
        <button>Add Move</button>
      </form>

      <AllMoves user={$user} />
    {/if}

  </main>
</Route>
<Route path="/tools">
  <h2>Tools</h2>
</Route>
