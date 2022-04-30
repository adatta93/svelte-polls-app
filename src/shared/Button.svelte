<script>
  export let type = "primary";
  export let flat = false;
  export let inverse = false;
</script>

<button class={type} class:flat={flat} class:inverse={inverse} on:click>
  <slot></slot>
</button>

<style>
  button {
    border: 0;
    border-radius: 6px;
    cursor: pointer;
    padding: 8px 12px;
    font-weight: bold;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.2);
  }
  .primary {
    background-color: #d91b42;
    color: white;
  }
  .primary:hover {
    background-color: #d70933;
  }
  .secondary {
    background-color: #45c496;
    color: white;
  }
  .secondary:hover {
    background-color: #1cc588;
  }
  .flat {
    box-shadow: none;
  }
  .primary.inverse {
    background-color: white;
    color: #d91b42;
    border: 2px solid #d91b42;
  }
  .primary.inverse:hover {
    background-color: #d91b42;
    color: white;
  }
  .secondary.inverse {
    background-color: white;
    color: #45c496;
    border: 2px solid #45c496;
  }
  .secondary.inverse:hover {
    background-color: #45c496;
    color: white;
  }
</style>