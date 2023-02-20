<script>
    import Icon from 'svelte-awesome';
    import chevronRight from 'svelte-awesome/icons/chevronRight';

    export let transactions;

    let name;
    let show = false;
    let loading = false;

    let iconOpen = false;

    if (transactions) {
        name = transactions[0].respresentative;
    }
    
    function dropDown() {
        iconOpen = !iconOpen;
        loading = !loading;
        setTimeout(()=> {
            show = !show;
        })
    }

</script>
<h3 on:keydown={dropDown} on:click={dropDown} class="purchaseTitle">Purchases
    <Icon data={chevronRight} style={`transform:rotate(${iconOpen ? 90 : 0}deg); transition: transform 150ms linear`}/>
</h3>
{#if show}
    <table class="table">
        <thead>
            <tr>
                <th scope="col">Ticker</th>
                <th scope="col">Date</th>
                <th scope="col">Asset</th>
                <th scope="col">Amount</th>
                <th scope="col">Sector</th>
                <th scope="col">Industry</th>
            </tr>
        </thead>
        <tbody>
            {#each transactions as transaction, i}
                {#if transaction.type === "purchase"}
                    <tr>
                        <th scope="row">${transaction.ticker}</th>
                        <td>{transaction.transaction_date}</td>
                        <td>{transaction.asset_description}</td>
                        <td>{transaction.amount}</td>
                        <td>
                            {#if transaction.sector}
                                {transaction.sector}
                            {:else}
                                unknown
                            {/if}
                        </td>
                        <td>
                            {#if transaction.industry}
                                {transaction.industry}
                            {:else}
                                unknown
                            {/if}
                        </td>
                    </tr>
                {/if}
            {/each}
        </tbody>
    </table>
{/if}
{#if loading && !show}
    <div class="spinner-border" role="status">
        <span class="visually-hidden">Loading...</span>
    </div>
{/if}
<style>
    .purchaseTitle {
        cursor: pointer;
    }
</style>