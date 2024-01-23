<script lang="ts">

  async function fetchData() {
    try {
      const res = await fetch('http://localhost:3000');
      const data = await res.json();
      return data;
    } catch (error) {
      console.error(error);
      throw error;
    }
  }

</script>

<main>
  {#await fetchData()}
    <p>Fetching Data</p>
  {:then data}
    {@const users = data.users}
    <ol>
    {#each users as user}
       <li>{user}</li>
    {/each}
    </ol>
  {:catch error}
    <!-- fetchData was rejected -->
  {/await}
</main>
