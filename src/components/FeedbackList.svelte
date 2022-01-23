<script>
  import FeebackItem from './FeedbackItem.svelte';

  export let feedback = [];
</script>

{#each feedback as fb (fb.id)}
  <FeebackItem item={fb} on:delete-fb />
{/each}

<style></style>
