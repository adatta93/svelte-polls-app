<script>
  import { createEventDispatcher } from "svelte";
  import { tweened } from "svelte/motion";
  import PollStore from "../stores/PollStore";
  import Button from "../shared/Button.svelte";

  export let poll;
  const dispatch = createEventDispatcher();

  // reactive values
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor(100 / totalVotes * poll.votesA) || 0;
  $: percentB = Math.floor(100 / totalVotes * poll.votesB) || 0;

  // tweened percent
  const tweenedA = tweened(0);
  const tweenedB = tweened(0);
  $: tweenedA.set(percentA);
  $: tweenedB.set(percentB);

  // poll voting
  const handleVote = (option, id) => {
    PollStore.update(currentPolls => {
      let copiedPolls = [...currentPolls];
      let votedPoll = copiedPolls.find(poll => poll.id === id);

      if(option === "a") {
        votedPoll.votesA++;
      } else {
        votedPoll.votesB++;
      }

      return copiedPolls;
    });
  }

  // Delete poll
  const handleDelete = (id) => {
    PollStore.update(currentPolls => {
      return currentPolls.filter(poll => poll.id !== id);
    });
  }
</script>

<div class="card">
  <div class="poll">
    <h3>{ poll.question }</h3>
    <p>Total Votes: {totalVotes}</p>
    <div class="answer" on:click={() => handleVote('a', poll.id)}>
      <div class="percent percent-a" style="width: {$tweenedA}%;"></div>
      <span>{ poll.answerA } ({poll.votesA})</span>
    </div>
    <div class="answer" on:click={() => handleVote('b', poll.id)}>
      <div class="percent percent-b" style="width: {$tweenedB}%;"></div>
      <span>{ poll.answerB } ({poll.votesB})</span>
    </div>

    <div class="delete">
      <Button inverse={true} flat={true} on:click={() => handleDelete(poll.id)}>Delete</Button>
    </div>
  </div>
</div>

<style>
  .card {
    background: #fff;
    padding: 20px;
    border-radius: 6px;
    box-shadow: 2px 0px 4px rgb(0, 0, 0, 0.1), 0 2px 6px rgb(0, 0, 0, 0.1);
  }
  h3 {
    margin: 0;
    color: #555;
  }
  p {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }
  .percent {
    position: absolute;
    height: 100%;
    box-sizing: border-box;
  }
  .percent-a {
    border-left: 4px solid #d91b42;
    background: rgba(217,27,66,0.2);
  }
  .percent-b {
    border-left: 4px solid #45c496;
    background: rgba(58,190,150,0.2);
  }
  .delete {
    margin-top: 30px;
    text-align: center;
  }
</style>