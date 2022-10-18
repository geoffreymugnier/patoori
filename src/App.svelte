<script>
  import { format } from 'date-fns';

  let displayingFuture = false;

  const riceDays = ["Monday", "Tuesday", "Thursday"];
  const pastaDays = ["Wednesday", "Friday"];

  const isRiceDay = () => {
    const today = new Date().getDay();
    const day = format(today, "EEEE")
    return riceDays.includes(day);
  }

  const nextPastaDay = () => {
    const today = new Date().getDay();
    const day = format(today, "EEEE")
    const nextDay = pastaDays.find(d => d > day);
    return nextDay;
  }

  const nextRiceDay = () => {
    const today = new Date().getDay();
    const day = format(today, "EEEE")
    const nextDay = riceDays.find(d => d > day);
    return nextDay;
  }

  const handleDisplayFuture = () => {
    displayingFuture = true;
    setTimeout(() => {
      displayingFuture = false;
    }, 3000);
  }
</script>

<nav>Patoori</nav>
{#if isRiceDay()}
  <h1>It's 🍚🐷 day!</h1>
  {#if displayingFuture}
    <p>It will be on <b>{nextPastaDay()}</b></p>
  {:else}
    <button on:click={handleDisplayFuture}>When's next 🍝 ?</button>
  {/if}
{:else}
  <h1>It's 🍝 day!</h1>
  {#if displayingFuture}
    <p>It will be on <b>{nextRiceDay()}</b></p>
  {:else}
    <button on:click={handleDisplayFuture}>When's next 🍚🐷 ?</button>
  {/if}
{/if}

<style>
  nav {
    padding: 1em;
    font-size: 1.5em;
    font-weight: bold;
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
