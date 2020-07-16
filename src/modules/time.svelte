<script>
  export let day = 1;

  function nextDay() {
    day += 1;
  }
</script>

<style>
  main {
    display: flex;
    flex-direction: column;
  }

  h1 {
    color: #ffffff;
    text-transform: uppercase;
    font-size: 24px;
    font-weight: 100;
    margin-top: 0;
    margin-bottom: 10px;
  }

</style>

<main>
  <h1>Day {day}</h1>
  <button on:click={() => nextDay()}>Rest a day</button>
</main>
