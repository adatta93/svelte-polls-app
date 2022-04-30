<script>
  //import { onDestroy } from "svelte";
  import { fade, slide, scale } from "svelte/transition";
  import { flip } from "svelte/animate";
  import PollStore from "../stores/PollStore.js";
  import PollDetails from "./PollDetails.svelte";

  // Use $PollStore instead of these lines
  /* export let polls = [];
  const unsub = PollStore.subscribe(data => {
    polls = data;
  });
  onDestroy(() => {
    unsub();
  }); */
</script>

<div class="poll-list">
  {#each $PollStore as poll (poll.id)}
    <div in:slide out:scale|local animate:flip={{duration: 500}}>
      <PollDetails {poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-top: 16px;
  }
</style>