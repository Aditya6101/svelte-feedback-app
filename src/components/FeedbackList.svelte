<script>
  import { fade, scale } from 'svelte/transition';
  import { FeedbackStore } from '../stores';
  import FeebackItem from './FeedbackItem.svelte';
</script>

{#each $FeedbackStore as fb (fb.id)}
  <div in:scale={{ duration: 500 }} out:fade={{ duration: 500 }}>
    <FeebackItem item={fb} on:delete-fb />
  </div>
{/each}

<style></style>
