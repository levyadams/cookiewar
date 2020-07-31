<script>
  export let locations;

  export let cookies;

  export let windowMessage = "";

  export let currentDay = 0;

  let cookieEvent = false;
  let cookieEventDaysUntil = 0;

  export const increaseMessages = [
    { 0: `Feminist convention in`, 1: `prices are empowered!` },
    { 0: `MRA convention in`, 1: `prices go their own way..up!` },
    { 0: `Communism convention in`, 1: `prices flourish!` },
    { 0: `Gaming convention in`, 1: `prices are epic rn` },
    { 0: `Anime convention in`, 1: `prices bulge oWo` },
    { 0: `Furry convention in`, 1: `*prices bulge* oWo` },
  ];
  export const decreaseMessages = [
    { 0: `overstock in`, 1: `prices drop.` },
    { 0: `Chinese regulations lifted in`, 1: `prices disappear.` },
    { 0: `Fat tax removed in`, 1: `prices are lower than life expectancy.` },
    { 0: `Local supplier closes doors in`, 1: `prices are low.` },
    {
      0: `Toxic sugar alternative deregulated in`,
      1: `prices artificially deflate.`,
    },
    { 0: `Local competition goes under in`, 1: `prices are in the ground.` },
  ];

  //cookie event handler
  $: {
    if (currentDay > 1) {
      rollForCookieEvent();
    }
    console.log(cookieEventDaysUntil);
    if (cookieEventDaysUntil > 0) {
      cookieEventDaysUntil = cookieEventDaysUntil - 1;
      if (cookieEventDaysUntil === 0) {
          console.log('set cookie prices!');
        setCookiePrices();
      }
    }

  }
  let weightedNumberGenerator = (spread, range, weight) => {
    let spreadVal = Math.round(Math.random() * 10);
    let rangeValue = Math.random() * (range[1] - range[0] + 1) + range[0];
    if (spreadVal <= spread) {
      let newVal = rangeValue * weight;
      return parseFloat(newVal.toFixed(2));
    } else {
      return parseFloat(rangeValue.toFixed(2));
    }
  };

  let weightedEventDayTimer = (val)=>{
      if(val >= 9 ){
          return 1;
      }
      else{
         return Math.round(Math.random() * Math.floor(val));
      }

  };

work with events so it flows well with a 45 day game trial
  //iterate through location.localPrices and set the towns
  //local cookie prices based on the weightedNumberGenerator.
  let setCookiePrices = () => {
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
  };
  //run this on start to set all cookie prices
  setCookiePrices();

  let rollForCookieEvent = () => {
    //each day, roll for cookie event. ~15% chance.
    let randyVal = parseFloat((Math.random() * 10).toFixed(2));
    if (randyVal >= 8.5) {
      let randyVal1 = parseFloat((Math.random() * 10).toFixed(2));
      if (currentDay < 15) {
          let cookieReturnVal = 0;
        if (randyVal1 >= 5) {
         cookieReturnVal = randomizeCookie(true);
        } else {
         cookieReturnVal = randomizeCookie(false);
        }
        cookieEvent = true;
        cookieEventDaysUntil = weightedEventDayTimer(cookieReturnVal);

      }
      //cookie events drop after day 15 for added difficulty 9% chance.
      else {
          let cookieReturnVal = 0;
        if (randyVal >= 9.1) {
         cookieReturnVal = randomizeCookie(true);
        } else {
        cookieReturnVal = randomizeCookie(false);
        }
        cookieEvent = true;
        cookieEventDaysUntil = weightedEventDayTimer(cookieReturnVal);


      }
    }
  };
  let randomizeCookie = (increase) => {
    let randoLocation = locations[Math.round(Math.random() * 3)];
    let randoCookie = randoLocation.localPrices[Math.round(Math.random() * 5)];

    if (increase) {
        windowMessage = returnRandoCookieMessage(
        true,
        randoLocation,
        randoCookie
    );
     return randoCookie.price = parseFloat(
        randoCookie.price * Math.round(Math.random() * 10).toFixed(2)
      );
      
    } else {
      let randyPrice = randoCookie.price / 3;
      windowMessage = returnRandoCookieMessage(
        false,
        randoLocation,
        randoCookie
      );
      return randoCookie.price = parseFloat(randyPrice.toFixed(2));
    }
  };

  let returnRandoCookieMessage = (increase, location, cookie) => {
    if (increase) {
      let oof = Math.floor(Math.random() * increaseMessages.length - 1);
      if (oof < 0) {
        oof = 0;
      }
      let message = increaseMessages[oof];
      return `${message[0]} ${location.name}, ${cookie.name} ${message[1]}`;
    } else {
      let oof = Math.floor(Math.random() * decreaseMessages.length - 1);
      if (oof < 0) {
        oof = 0;
      }
      let message = decreaseMessages[oof];
      return `${message[0]} ${location.name}, ${cookie.name} ${message[1]}`;
    }
  };
</script>

<style>
  .hidden {
    display: none;
  }
</style>

<main />
