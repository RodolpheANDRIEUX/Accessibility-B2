<script>
	export let data;
	import comment from '$lib/images/comment.svg';
</script>

<svelte:head>
	<title>Blog</title>
	<meta name="description" content="Un blog accessible de fou" />
</svelte:head>

<h1 class="visually-hidden">Titre de la page</h1>

<picture>
	<source class="bg-decorations coffee1" media="(min-width: 1000px)" type="image/webp" srcset="/src/lib/images/coffee1.webp" />
	<img role="presentation" class="bg-decorations coffee1" src="/src/lib/images/coffee1.png" alt="coffee" />
</picture>
<picture>
	<source class="bg-decorations coffee" media="(min-width: 1000px)" type="image/webp" srcset="/src/lib/images/coffee.webp" />
	<img role="presentation" class="bg-decorations coffee" src="/src/lib/images/coffee.png" alt="more coffee" />
</picture>


<section>
	{#each data.posts as post}
		<a class="article-link" href="/article/{post.id}">
			<article aria-labelledby="title-{post.id}">
				<div role="article">
					<h2 id="title-{post.id}" style="view-transition-name: {post.title};">{post.title}</h2>
					<p style="view-transition-name: {post.id}-content;">{@html post.content}</p>
				</div>
				{#if post.image}
					<picture style="view-transition-name: {post.image.imageName};">
						<source media="(min-width: 1000px)" type="image/webp" srcset="/src/lib/images/{post.image.imageName}/{post.image.imageName}-100.webp" /> <!-- 100% quality -->
						<source media="(min-width: 600vh)" type="image/webp" srcset="/src/lib/images/{post.image.imageName}/{post.image.imageName}-75.webp" /> <!-- 75% quality -->
						<source type="image/webp" srcset="/src/lib/images/{post.image.imageName}/{post.image.imageName}-20.webp" />	<!-- 20% quality -->
						<img src="/src/lib/images/{post.image.imageName}/{post.image.imageName}.jpg" alt={post.image.imageAlt} /> <!-- Fallback -->
					</picture>
				{/if}
			</article>
		</a>
		{#if post.comments}
			<a href="/article/{post.id}#comments">
				<aside>
					<img class="comments-icon" src={comment} alt="comment-icon" />
					<p class="comments">{post.comments.length} comments</p>
				</aside>
			</a>

		{/if}
	{/each}
</section>

<style>
	section {
		padding: 5rem 0;
	}

	.bg-decorations {
		z-index: -1;
		position: absolute;
		width : 15%;
	}

	.coffee1 {
		top: 100px;
		left: 2%;
		scale: 1.2;
	}

	.coffee {
		bottom: 200px;
		right: 2%;
		scale: .8;
		opacity: .8;
	}

	@media (max-width: 1700px) {
		.bg-decorations {
			width : 10%;
		}
	}

	@media (max-width: 1350px) {
		.bg-decorations {
			display: none;
		}
	}

	aside {
		margin-left: 2rem;
		display: flex;
		gap: 0.8rem;
		align-items: center;
	}

	a {
		color: inherit;
	}

	.comments-icon {
		width: 1.8rem;
	}

	.comments {
		opacity: .5;
		font-size: 1.2rem;
	}

	.article-link {
		color: inherit;
		text-decoration: none;
	}

	article {
		transition: .3s;
		display: flex;
		flex-direction: row;
		gap: 5%;
		padding: 1rem;
		margin-top: 3rem;
		box-shadow: #444444 -1px 3px 6px -5px;
		border-top: transparent 2px solid;
	}

	@media (max-width: 600px) {
		article {
			flex-direction: column;
		}
	}

	article:hover {
		transform: translateY(-5px);
		border-top: var(--color-theme-1) 2px solid;
		background-color: #f0f0f0f0;
		box-shadow: #444444 -1px 3px 6px -5px;
	}

	article > div {
		flex: 3;
	}

	h2 {
		margin-bottom: 0.5rem;
		font-size: 1.5rem;
		font-weight: 600;
	}

	picture {
		flex: 2;
		max-height: 250px;
		overflow: hidden;
	}

	article	img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.visually-hidden {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		margin: -1px;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		border: 0;
	}
</style>
