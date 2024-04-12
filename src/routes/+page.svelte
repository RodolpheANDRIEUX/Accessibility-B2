<script>
	export let data;
</script>

<svelte:head>
	<title>Blog</title>
	<meta name="description" content="Un blog accessible de fou" />
</svelte:head>

<section>
	{#each data.posts as post}
		<a href="/article/{post.id}">
			<article>
				<div>
					<h2>{post.title}</h2>
					<p>{@html post.content}</p>
				</div>
				{#if post.image}
					<picture>
						<source type="image/webp" srcset={post.image.imageLink} />
						<img src="../lib/images/{post.image.imageFile}" alt={post.image.imageAlt} />
					</picture>
				{/if}
			</article>
		</a>
	{/each}

</section>

<style>
	section {
		padding-top: 50px;
	}

	a {
		text-decoration: none;
		color: inherit;
	}

	article {
		transition: .3s;
		display: flex;
		gap: 5%;
		margin-bottom: 5rem;
		padding: 1rem;
		box-shadow: #444444 -1px 3px 6px -5px;
	}

	article:hover {
		transform: translateY(-5px);
		border-top: var(--color-theme-1) 2px solid;
		background-color: #f0f0f0f0;
		box-shadow: #444444 -1px 3px 6px -5px;
	}

	article > div {
		flex: 2;
	}

	h2 {
		margin-bottom: 0.5rem;
		font-size: 1.5rem;
	}

	picture {
		flex: 1;
	}

	img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}
</style>
