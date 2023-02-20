<script>
    export let transactions;
    let name
    if (transactions) {
        name = transactions[0].respresentative;
    }
    console.log(transactions)
</script>
{#if transactions}
    <h3>Purchases</h3>
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