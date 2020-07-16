<script>
  import { cash,owned_chipz,owned_mintz,owned_semonas,owned_shmores,owned_wagalongs,owned_patties } from "./../stores/store.js";
  import { locations as _locations, cookies as _cookies } from "./dataObjects.svelte";
  import CookieButton from './cookieButton.svelte';
  import MarketWindow from './marketWindow.svelte';
  import LocationsWindow from './locationsWindow.svelte';


  let locations = _locations;
  let cookies = _cookies;

  let itemExpanded = false;

  export const currentArea = locations[0];

  let marketWindow;
  let marketWindowClosed = true;
  let marketWindowTitle;
  let marketWindowIcon;
  let windowCookiePrice;
  let cookiesOwned;

  let locationsWindow;

 
  //working with stores inside of svelte. Works great for global
  //data that is too distant from each other to simply raise state
  function addOrRemoveCash(val, add) {
    if (add) {
      cash.update((n) => n + val);
    } else {
      cash.update((n) => n - val);
    }
  }
  //iterate through location.localPrices and set the towns
  //local cookie prices based on the weightedNumberGenerator.
  function setCookiePrices() {
    locations.map((location) => {
      location.localPrices.map((cookiePrice) => {
        cookies.map((cookie) => {
          if (cookie.name === cookiePrice.name) {
            cookiePrice.price = weightedNumberGenerator(
              location.priceSpread,
              [cookie.minPrice, cookie.maxPrice],
              location.cookieWeight
            );
            locations = [...locations];
          }
        });
      });
    });
  }
  function setCookieLabel(cookieName){
    switch(cookieName){
        case 'chipz':
            return $owned_chipz;
        break;

        case 'semonas':
            return $owned_semonas;
        break;

        case 'wagalongs':
            return $owned_wagalongs;
        break;

        case 'shmores':
            return $owned_shmores;
        break;

        case 'patties':
            return $owned_patties;
        break;

        case 'mintz':
            return $owned_mintz;
        break;

    }
};
function setCookieIcon(cookieName){
     switch(cookieName){
        case 'chipz':
            return 'icon-spinner5';
        break;

        case 'semonas':
            return 'icon-spinner5';
        break;

        case 'wagalongs':
            return 'icon-spinner5';
        break;

        case 'shmores':
            return 'icon-spinner5';
        break;

        case 'patties':
            return 'icon-spinner5';
        break;

        case 'mintz':
            return 'icon-spinner5';
        break;

    }
}
  //remove
  setCookiePrices();

//#region weighted Generator summary
  //each town has a weight as to whether or not it will behave
  //within its usual price ranges or behave completely randomly.
  //the higher the spread value, the less likely the generator to
  //generate very random values. The range is the min and max values
  //to generate the number between. The weight floats around 1,
  // .75 would be a town with cheaper cookie prices on average
  // than a town with a weight of 1.5. This value can also be exagerrated
  // down the road for game events like cookie shortages and such.
//#endregion
  function weightedNumberGenerator(spread, range, weight) {
    let spreadVal = Math.round(Math.random() * 10);
    let rangeValue = Math.floor(
      Math.random() * (range[1] - range[0] + 1) + range[0]
    );
    if (spreadVal <= spread) {
      return rangeValue * weight;
    } else {
      return rangeValue;
    }
  }

  function toggleCookieWindow(cookieName,cookiePrice,ownedCookies){
      marketWindowTitle = cookieName;
      windowCookiePrice = cookiePrice;
      cookiesOwned = translateStringToStore(cookieName);

      if(marketWindowClosed){
          marketWindowClosed = false;
      }
      else{
          marketWindowClosed = true;
      }
  }
  function translateStringToStore(string){
      switch(string){
          case 'semonas':
              return $owned_semonas;
            break;

        case 'mintz':
              return $owned_mintz;
            break;

        case 'wagalongs':
              return $owned_wagalongs;
            break;

         case 'chipz':
              return $owned_chipz;
            break;
        
        case 'shmores':
              return $owned_shmores;
            break;

        case 'patties':
            return $owned_patties;
        break;


      }
  }

</script>

<main>
<MarketWindow 
bind:hidden={marketWindowClosed}
bind:this={marketWindow}
windowTitle = {marketWindowTitle}
windowIcon = {marketWindowIcon}
cash = {$cash}
 cookiePrice = {windowCookiePrice}
boxesOwned = {cookiesOwned}
/>
  <h2>{currentArea.name}</h2>
  <!-- <button on:click={() => addOrRemoveCash(5, true)}>Add cash!</button> -->
  <!-- <button on:click={() => addOrRemoveCash(5, false)}>Remove cash!</button> -->
  <!-- <button on:click={() => setCookiePrices()}>Fill location prices</button> -->
  <div  class="cookie-container">
   {#each locations as location}
    {#each location.localPrices as cookie}
    <CookieButton
    on:click={el=>toggleCookieWindow(cookie.name,cookie.price)} 
    cookieLabel={cookie.name}
    cookiePrice={cookie.price}
    icon={setCookieIcon(cookie.name)}
    ownedIcon={cookie.ownedIcon}
    ownedLabel={setCookieLabel(cookie.name)}
    />
    {/each}
  {/each}
  </div>
 
 <LocationsWindow 
  locations ={locations}
 />
</main>

<style>
  p,
  h2 
  {
    margin:0 0 15px 0;
    color: rgb(255, 255, 255);
  }
  .cookie-container{
      display: flex;
      flex-wrap:wrap;
      background:rgb(255, 255, 255);
      border-radius:5px;
  }

</style>