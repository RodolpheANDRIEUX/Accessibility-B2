<script>
    export let data;
    import { onMount } from 'svelte';
    import Table from './Table.svelte';

    let button;
    let dialog;

    onMount(() => {
        button = document.querySelector('button');
        dialog = document.querySelector('dialog');

        if (button === null || dialog === null) {
            return;
        }

        dialog.addEventListener('click', () => {
            dialog.close();
        });
    });

</script>

<svelte:head>
    <title>{data.title}</title>
    <meta name="description" content="Article de blog {data.title}" />
</svelte:head>

<section>
    <article>
        <div>
            <h1>{data.title}</h1>
            <p>{@html data.content}</p>
        </div>
        {#if data.image}
            <dialog>
                <img src="/src/lib/images/{data.image.imageName}/{data.image.imageName}-100.webp" alt={data.image.imageAlt} />
            </dialog>
            <button on:click={() => dialog.showModal()} on:keydown={(event) => { if (event.key === 'Enter') dialog.showModal(); }}>
                <picture style="view-transition-name: {data.image.imageName};">
                    <source media="(min-width: 1000px)" type="image/webp" srcset="/src/lib/images/{data.image.imageName}/{data.image.imageName}-100.webp" /> <!-- 100% quality -->
                    <source media="(min-width: 600px)" type="image/webp" srcset="/src/lib/images/{data.image.imageName}/{data.image.imageName}-75.webp" /> <!-- 75% quality -->
                    <source type="image/webp" srcset="/src/lib/images/{data.image.imageName}/{data.image.imageName}-20.webp" /> <!-- 20% quality -->
                    <img src="/src/lib/images/{data.image.imageName}/{data.image.imageName}.jpg" alt={data.image.imageAlt} /> <!-- Fallback -->
                </picture>
            </button>
        {/if}
    </article>
</section>

<section>
    <h2 id="comments">Comments</h2>
    {#if data.comments && data.comments.length > 0}
        {#each data.comments as comment}
            <article id="comment">
                <h3>{comment.author}</h3>
                <p>{comment.content}</p>
            </article>
        {/each}
    {:else}
        <p>there is no comment for this article.</p>
    {/if}
</section>

<section>
    <h2>Tableau</h2>
    <Table {data} />
</section>


<style>
    section {
        margin-bottom: 3rem;
    }

    article {
        margin: 0 auto;
        max-width: 1140px;
    }

    h1 {
        margin-bottom: 3rem;
        font-size: 3rem;
        font-weight: 600;
    }

    h2 {
        margin-bottom: 1rem;
        font-size: 2rem;
        font-weight: 500;
    }

    h3 {
        margin-bottom: .8rem;
    }

    p {
        box-shadow: #444444 -3px -3px 6px -5px;
        backdrop-filter: blur(5px);
        border-left: var(--color-theme-1) 2px solid;
        padding: 1rem;
        line-height: 1.5;
    }

    #comment p {
        margin: 0 0 2rem 1rem;
    }

    button {
        border: 0;
        background-color: transparent;
        cursor: pointer;
        padding: 0;
        margin: 0;
    }

    dialog {
        max-width: 95%;
        max-height: 90%;
        background-color: #aaaaaa40;
        backdrop-filter: blur(5px);
        border: 0;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        animation: fadeFromBottom .3s;
    }

    @keyframes fadeFromBottom {
        from {
            transform: translateY(10%);
            opacity: 0;
        }
        to {
            transform: translateY(0);
            opacity: 1;
        }
    }

    dialog img {
        max-width: 89vw;
        max-height: 89vh;
    }

    img {
        max-width: 100%;
    }
</style>