<script>
    //Lloyd Doggett
    import Icon from 'svelte-awesome';
    import chevronRight from 'svelte-awesome/icons/chevronRight';
    import ibm from '../ibm.json';
    import SuccessGraph from './SuccessGraph.svelte';
    export let transactions;

    let name;
    let show = false;
    let loading = false;

    let iconOpen = false;

    export let selected;
    let data=[]

    $:if (transactions) {
        name = transactions[0].respresentative;
        transactions.forEach((transaction) => {
            if (transaction.ticker === "IBM") {

            }
        })
    }
    
    function dropDown() {
        iconOpen = !iconOpen;
        loading = !loading;
        setTimeout(()=> {
            show = !show;
        })
    }

</script>
<h3 on:keydown={dropDown} on:click={dropDown} class="purchaseTitle">Transactions
    <Icon data={chevronRight} style={`transform:rotate(${iconOpen ? 90 : 0}deg); transition: transform 150ms linear`}/>
</h3>
{#if show}
    {#if selected}
        <p>placeholder</p>
    {:else}
        <p>Please select a representative first as to prevent request spamming to data api</p>
    {/if}
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