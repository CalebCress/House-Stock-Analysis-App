<script>
    import { afterUpdate } from 'svelte';
    import Icon from 'svelte-awesome';
    import chevronRight from 'svelte-awesome/icons/chevronRight';

    export let transactions;

    let stocks = new Map();
    let favourites = [];

    function updateTransactions() {
        favourites = [];
        stocks = new Map();
        transactions.forEach(transaction => {
            if (transaction.asset_description){
                if (stocks.get(transaction.asset_description.replace('.',''))) {
                    stocks.get(transaction.asset_description.replace('.','')).count++;
                } else {
                    stocks.set(transaction.asset_description.replace('.',''), {
                        count: 1,
                        ticker: transaction.ticker
                    })
                    favourites.push(transaction.asset_description.replace('.',''))
                }
            }
        });

        favourites.sort((a, b) => {
            return stocks.get(b).count - stocks.get(a).count;
        })
    }

    $:if (transactions) {
        updateTransactions();
    }
    let show = false;
    let loading = false;

    let iconOpen = false;
    
    function dropDown() {
        iconOpen = !iconOpen;
        loading = !loading;
        setTimeout(()=> {
            show = !show;
        })
    }
</script>
<h3 on:keydown={dropDown} on:click={dropDown} class="favouritesTitle">Favourites
    <Icon data={chevronRight} style={`transform:rotate(${iconOpen ? 90 : 0}deg); transition: transform 150ms linear`}/>
</h3>
{#if show}
    {#each favourites as fav,i}
        <p>{i+1}. {fav}</p>
    {/each}
{/if}
{#if loading && !show}
    <div class="spinner-border" role="status">
        <span class="visually-hidden">Loading...</span>
    </div>
{/if}
<style>
    .favouritesTitle {
        cursor: pointer;
    }
</style>