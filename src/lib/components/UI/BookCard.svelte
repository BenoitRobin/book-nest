<script lang="ts">
	import type { Book } from '$lib/state/user-state.svelte';
	import StarRating from './StarRating.svelte';

	interface BookCardProps {
		book: Book;
	}

	let { book }: BookCardProps = $props();

	let bookStatus = $derived(
		book.finished_reading_on
			? 'Finished'
			: book.started_reading_on
				? 'Currently reading'
				: 'Not started'
	);
</script>

<a href={`/private/books/${book.id}`} class="book-card">
	<div class="book-status">
		<span>{bookStatus}</span>
	</div>
	<div class="book-cover">
		{#if book.cover_image}
			<img src={book.cover_image} alt={book.title} />
		{/if}
	</div>
	<div class="book-info">
		<h4>{book.title}</h4>
		<p class="mb-s">{book.author}</p>
		<StarRating isReadOnly={true} value={book.rating || 0} />
	</div>
</a>

<style>
	.book-card {
		position: relative;
		display: flex;
		flex-direction: column;
		width: 100%;
		min-width: 220px;
		width: 220px;
		height: 300px;
		max-width: 450px;
		border-radius: 12px;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		color: #fff;
		text-decoration: none;
		text-align: left;
	}

	.book-cover {
		position: absolute;
		width: 100%;
		height: 100%;
		z-index: -1;
	}

	.book-cover img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 12px;
	}

	.book-info {
		background: rgba(0, 0, 0, 0.4);
		width: 100%;
		height: 100%;
		padding: 170px 16px 0 16px;
		border-radius: 12px;
	}
	.book-info h4 {
		font-family: 'EB Garamond', serif;
		font-size: 20px;
	}
	.book-info p {
		font-size: 14px;
		font-weight: 400;
		font-style: italic;
	}
	.book-status {
		position: absolute;
		top: 16px;
		right: 5px;
		padding: 4px 8px;
		width: auto;
		background-color: rgba(4, 59, 92, 0.7);
		border-radius: 12px;
	}
</style>
