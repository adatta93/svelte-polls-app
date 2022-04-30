<script>
import { createEventDispatcher } from "svelte";


  export let tabs;
  export let activeTab;

  const dispatch = createEventDispatcher();
</script>

<nav>
  {#each tabs as tab}
    <div class:active={activeTab === tab} on:click={() => dispatch("tabChange", tab)}>{tab}</div>
  {/each}
</nav>

<style>
  nav {
    display: flex;
    justify-content: center;
  }
  div {
    margin: 0 16px;
    font-size: 18px;
    color: #555;
    cursor: pointer;
  }
  div:hover {
    color: #ff1343
  }
  div.active {
    color: #d91b42;
    border-bottom: 2px solid #d91b42;
    padding-bottom: 8px;
  }
</style>