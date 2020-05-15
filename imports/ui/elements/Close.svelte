<script>
  export let text = "&times;";
</script>

<style>
  button {
    border: 0;
    border-radius: 50%;
    color: var(--white);
    background: var(--red);
    box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.2);
  }
</style>

<button>
  {@html text}
</button>
