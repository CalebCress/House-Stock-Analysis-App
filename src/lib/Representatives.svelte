<script>
    export let data;

    let representatives = [];

    data.forEach(transaction => {
        if (!representatives.includes(transaction.representative)) {
            representatives.push(transaction.representative)
        }
    })
</script>

<main>
    {#each representatives as representative}
        <p>{representative}</p>
    {/each}
</main>