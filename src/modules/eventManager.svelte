<main>
</main>
<script>
    export let locations;

    export let windowMessage = '';

    export let currentDay = 0;
    export const increaseMessages=[
        {0:`Feminist convention in`,1:`prices are empowered!`},
        {0:`MRA convention in`,1:`prices go their own way..up!`},
        {0:`Communism convention in`,1:`prices flourish!`},
        {0:`Gaming convention in`,1:`prices are epic rn`},
        {0:`Anime convention in`,1:`prices bulge oWo`},
        {0:`Furry convention in`,1:`*prices bulge* oWo`}
    ];
    export const decreaseMessages=[
        {0:`overstock in`,1:`prices drop.`},
        {0:`Chinese regulations lifted in`,1:`prices disappear.`},
        {0:`Fat tax removed in`,1:`prices are lower than life expectancy.`},
        {0:`Local supplier closes doors in`,1:`prices are low.`},
        {0:`Toxic sugar alternative deregulated in`,1:`prices artificially deflate.`},
        {0:`Local competition goes under in`,1:`prices are in the ground.`}
    ];

    //cookie event handler
    $:{
        let randyVal = Math.round(Math.random() * 10);
        if(randyVal > 8){
            let randyVal1 = Math.round(Math.random() * 10);
           if(currentDay<15){
              if(randyVal1<=5){
                  randomizeCookie(true);
              }
              else{randomizeCookie(false);}
           }
        }

    }
    let randomizeCookie=(increase)=>{
        let randoLocation = locations[Math.round(Math.random() * 3)];
        let randoCookie = randoLocation.localPrices[Math.round(Math.random() * 5)];

        if(increase){
            randoCookie.price = parseFloat(randoCookie.price * Math.round(Math.random()*10).toFixed(2));
            windowMessage = returnRandoCookieMessage(true,randoLocation,randoCookie);
        }
        else{
            let randyPrice = randoCookie.price / 3;
            randoCookie.price = parseFloat(randyPrice.toFixed(2));
            windowMessage = returnRandoCookieMessage(false,randoLocation,randoCookie);
        }
    };

    let returnRandoCookieMessage=(increase,location,cookie)=>{
        if(increase){
           let oof = Math.floor(Math.random()*increaseMessages.length - 1);
           if(oof <0){
               oof = 0;
           }
           let message = increaseMessages[oof];
            return `${message[0]} ${location.name}, ${cookie.name} ${message[1]}`;
        }
        else{
           let oof = Math.floor(Math.random()*decreaseMessages.length - 1);
           if(oof <0){
               oof = 0;
           }
           let message = decreaseMessages[oof];
            return `${message[0]} ${location.name}, ${cookie.name} ${message[1]}`;
        }
    }

   
</script>

<style>
.hidden{
    display:none;
}
</style>