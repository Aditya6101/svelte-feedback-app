<script>
  import { fade, scale } from 'svelte/transition';
  import FeebackItem from './FeedbackItem.svelte';

  export let feedback = [];
</script>

{#each feedback as fb (fb.id)}
  <div in:scale={{ duration: 500 }} out:fade={{ duration: 500 }}>
    <FeebackItem item={fb} on:delete-fb />
  </div>
{/each}

<style></style>
