<script>
  import { format } from "date-fns";

  let displayingFuture = false;

  const daysOrder = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"];
  const riceDays = ["Monday", "Tuesday", "Thursday"];
  const pastaDays = ["Wednesday", "Friday"];

  const today = new Date();
  const day = format(today, "EEEE");
  const currentDayIndex = daysOrder.indexOf(day);

  const isRiceDay = () => {
    return riceDays.includes(day);
  };

  const nextPastaDay = () => {
    const nextPastaDay = pastaDays.find((pastaDay) => {
      const pastaDayIndex = daysOrder.indexOf(pastaDay);
      return pastaDayIndex > currentDayIndex;
    });

    if (!nextPastaDay) {
      return pastaDays[0];
    }

    return nextPastaDay;
  };

  const nextRiceDay = () => {
    const nextRiceDay = riceDays.find((riceDay) => {
      const riceDayIndex = daysOrder.indexOf(riceDay);
      return riceDayIndex > currentDayIndex;
    });

    if (!nextRiceDay) {
      return riceDays[0];
    }

    return nextRiceDay;
  };

  const handleDisplayFuture = () => {
    displayingFuture = true;
    setTimeout(() => {
      displayingFuture = false;
    }, 3000);
  };
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

{#if day == "Friday"}
  <p>Have a nice weekend !</p>
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
