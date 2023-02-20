<script>
    export let data;
    export let currentRepData;

    let representatives = [];
    let rep;
    data.forEach(transaction => {
        if (!representatives.includes(transaction.representative)) {
            representatives.push(transaction.representative)
        }
    })

    function getRepData() {
        currentRepData = [];
        data.forEach(transaction => {
            if (transaction.representative === rep) {
                currentRepData.push(transaction)
            }
        })
        currentRepData = currentRepData;
    }
</script>

<main>
    <select bind:value={rep} class="form-select" aria-label="Default select example">
        <option disabled selected>Select Representative</option>
        {#each representatives as representative}
            <option value={representative}>{representative}</option>
        {/each}
    </select>
</main>