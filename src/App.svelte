<script lang="ts">
  import moment from "moment";
  import localforage from "localforage";
  import { onMount } from "svelte";
  let count: number = 0;
  const relativeTime = moment("20250212", "YYYYMMDD").fromNow();
  onMount(async () => {
    count = await localforage.getItem('count')
  });
  const handleClick = async () => {
    count++;
    await localforage.setItem('count', count);
  };
  const handleClickMinus = async () => {
    count--;
    await localforage.setItem('count', count);
  };
</script>

<main>
  <h1>Chocolates For Me!</h1>
  <p>Chocolates {relativeTime} (feb 12)</p>
  <button on:click={handleClick}>
    Add :)
  </button>
  <button on:click={handleClickMinus}>
    Decrease :(
  </button>
  <p>Total massed chocolates <strong>{count}</strong></p>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
