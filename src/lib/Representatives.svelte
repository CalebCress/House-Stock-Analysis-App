<script>
    export let data;
    export let currentRepData;

    let representatives = [];
    currentRepData = data;
    let rep = "All";
    data.forEach(transaction => {
        if (!representatives.includes(transaction.representative)) {
            representatives.push(transaction.representative)
        }
    })

    function getRepData() {
        currentRepData = [];
        if (rep === "All") {
            currentRepData = data;
        } else {
            data.forEach(transaction => {
                if (transaction.representative === rep) {
                    currentRepData.push(transaction)
                }
            })
        }
        // console.log(currentRepData)
        currentRepData = currentRepData;
    }
</script>

<main>
    <select bind:value={rep}  on:change={getRepData} class="form-select" aria-label="Default select example">
        <option selected>All</option>
        {#each representatives as representative}
            <option>{representative}</option>
        {/each}
    </select>
</main>

<style>
    select {
        width: auto;
    }
</style>