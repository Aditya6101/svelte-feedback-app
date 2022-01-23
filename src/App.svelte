<script>
  import FeedbackForm from './components/FeedbackForm.svelte';
  import FeedbackList from './components/FeedbackList.svelte';
  import FeedbackStats from './components/FeedbackStats.svelte';

  let feedback = [
    {
      id: 1,
      rating: 10,
      text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
    },
    {
      id: 2,
      rating: 9,
      text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
    },
    {
      id: 3,
      rating: 8,
      text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
    },
  ];

  $: count = feedback.length;
  $: average = feedback.reduce((acc, { rating }) => acc + rating, 0) / count;

  const addFb = (e) => (feedback = [e.detail, ...feedback]);

  const deleteFb = (e) =>
    (feedback = feedback.filter((fb) => fb.id !== e.detail));
</script>

<main class="container">
  <FeedbackForm on:add-feedback={addFb} />
  <FeedbackStats {count} {average} />
  <FeedbackList {feedback} on:delete-fb={deleteFb} />
</main>

<style>
</style>
