<script>
  import { FeedbackStore } from '../stores';
  import { v4 as uuidv4 } from 'uuid';

  import Card from './ui/Card.svelte';
  import Button from './Button.svelte';
  import RatingSelect from './RatingSelect.svelte';

  let text = '';
  let rating = 10;
  let btnDisabled = true;
  let min = 10;
  let msg = '';

  const handleInput = () => {
    if (text.trim().length <= min) {
      btnDisabled = true;
      msg = `Text must be at least ${min} characters`;
    } else {
      msg = null;
      btnDisabled = false;
    }
  };

  const handleSubmit = () => {
    if (text.trim().length >= min) {
      const newFeedback = {
        id: uuidv4(),
        text,
        rating: +rating,
      };
      FeedbackStore.update((currentFeedback) => [
        newFeedback,
        ...currentFeedback,
      ]);
      text = '';
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={({ detail }) => (rating = detail)} />
    <div class="input-group">
      <input
        type="text"
        on:input={handleInput}
        bind:value={text}
        placeholder="Tell us something that keeps you coming back"
      />
      <Button type="submit" disabled={btnDisabled}>Send</Button>
    </div>
    {#if msg}
      <p class="message">{msg}</p>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
