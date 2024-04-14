<script>
    export let data;
    import { onMount } from 'svelte';

    let picture;
    let dialog;

    onMount(() => {
        picture = document.querySelector('picture');
        dialog = document.querySelector('dialog');

        if (picture === null || dialog === null) {
            return;
        }

        picture.addEventListener('click', () => {
            dialog.showModal();
        });

        dialog.addEventListener('click', () => {
            dialog.close();
        });

        dialog.addEventListener('show', (event) => {
            event.preventDefault();
        });
    });

</script>

<svelte:head>
    <title>{data.title}</title>
    <meta name="description" content="Article de blog {data.title}" />
</svelte:head>

<article>
    <div>
        <h2>{data.title}</h2>
        <p>{@html data.content}</p>
    </div>
    {#if data.image}
        <dialog>
            <img src="/src/lib/images/{data.image.imageName}/{data.image.imageName}-100.webp" alt={data.image.imageAlt} />
        </dialog>
        <picture style="view-transition-name: {data.image.imageName};">
            <source media="(min-width: 1000px)" type="image/webp" srcset="/src/lib/images/{data.image.imageName}/{data.image.imageName}-100.webp" /> <!-- 100% quality -->
            <source media="(min-width: 600px)" type="image/webp" srcset="/src/lib/images/{data.image.imageName}/{data.image.imageName}-75.webp" /> <!-- 75% quality -->
            <source type="image/webp" srcset="/src/lib/images/{data.image.imageName}/{data.image.imageName}-20.webp" />	<!-- 20% quality -->
            <img src="/src/lib/images/{data.image.imageName}/{data.image.imageName}.jpg" alt={data.image.imageAlt} /> <!-- Fallback -->
        </picture>
    {/if}
</article>

<style>
    article {
        margin: 0 auto;
        max-width: 800px;
    }

    h2 {
        margin-bottom: 3rem;
        font-size: 3rem;
        font-weight: 600;
    }

    p {
        box-shadow: #444444 -3px -3px 6px -5px;
        backdrop-filter: blur(5px);
        border-left: var(--color-theme-1) 2px solid;
        padding: 1rem;
        line-height: 1.5;
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