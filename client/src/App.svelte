<script>
  import { onMount } from 'svelte'
  let usersList
  async function fetchData() {
    try {
      const res = await fetch('http://localhost:3000/'); // Include the protocol and the full path
      console.log(res);
      const data = await res.json();
      console.log(data);
      return data;
    } catch (error) {
      console.error(error);
      throw error; // Rethrow the error to trigger the catch block in the template
    }
  }

  onMount( async () => {
    usersList = await fetchData()
  })
</script>

<main>
  {#await usersList}
    <p>Fetching Data</p>
  {:then users}
    <!-- <ol>
      {#each users as user}
        <li>{user}</li>
      {/each}
    </ol> -->
    {@debug users}
  {:catch error}
    <p>Something went wrong! {error.message}</p>
  {/await}
</main>
