<script>
  export let text = "&times;";
</script>

<style>
  button {
    border: 0;
    border-radius: 50%;
    height: 26px;
    width: 26px;
    padding: 0;
    text-align: center;
    color: var(--white);
    background: var(--red);
    box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.2);
  }
</style>

<button>
  {@html text}
</button>
