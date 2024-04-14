<script>
    let articles = [
        {id: 1, name: 'Article A', value: 100, description: 'Description de l\'article A.'},
        {id: 2, name: 'Article B', value: 200, description: 'Description de l\'article B.'},
        {id: 3, name: 'Article C', value: 300, description: 'Description de l\'article C.'},
        {id: 4, name: 'Article D', value: 400, description: 'Description de l\'article D.'},
        {id: 5, name: 'Article E', value: 500, description: 'Description de l\'article E.'},
    ];
</script>

<table aria-describedby="Useless-Table">
    <caption id="Useless-Table">Un tableau vachement utile</caption>
    <thead>
    <tr>
        <th scope="col">ID</th>
        <th scope="col">Nom</th>
        <th scope="col">Valeur</th>
        <th scope="col">Description</th>
    </tr>
    </thead>
    <tbody>
    {#each articles as article (article.id)}
        <tr>
            <td>{article.id}</td>
            <td>{article.name}</td>
            <td>{article.value}</td>
            <td>{article.description}</td>
        </tr>
    {/each}
    </tbody>
</table>

<style>
    caption {
        font-size: 1.5em;
        font-weight: bold;
        margin-bottom: 10px;
    }

    table {
        margin: 30px 0;
        width: 100%;
        border-collapse: collapse;
        border-top: solid 2px var(--color-theme-1);
    }
    th, td {
        border: 1px solid black;
        padding: 8px;
        text-align: left;
        transition: .3s;
    }

    td:hover {
        background-color: #f2f2f2a0;
        scale: 1.1;
        transform: translate(5%, 0);
    }

    td:nth-child(1):hover  {
        background-color: #f2f2f2;
    }

    th {
        background-color: #f2f2f2;
    }
</style>