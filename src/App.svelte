<script>
  import Representatives from './lib/Representatives.svelte';
  async function getData() {
  const response = await fetch("https://house-stock-watcher-data.s3-us-west-2.amazonaws.com/data/all_transactions.json")
  const resData = await response.json();
  if (response.ok) {
    return resData;
  } else {
    throw new Error(resData);
  }
	}

  let data = getData();
  let currentRepData = [];
</script>
<main>
  {#await data}
    <div class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  {:then trans}
    <Representatives data={trans} bind:currentRepData/>
  {:catch error}
    <div class="alert alert-danger" role="alert">
      {error.message}
    </div>
  {/await}
</main>

<style>
</style>
