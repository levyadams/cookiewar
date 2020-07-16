<main>
    <div class="market-container" class:switched={buying} class:hidden={hidden}>
     <div class="layout-container">
      <h2>{windowTitle}</h2>
      <div class="{windowIcon}"></div>
      <p>$: {cookiePrice}</p>
      <p>boxes owned: {boxesOwned}</p>
      <p>currently: {buying ? 'buying' : 'selling'}</p>
      <label class="switch">
          <input class="custom" on:click={()=>{switchMarketState()}} type="checkbox">
          <span class="slider"></span>
      </label>
      <p>{buySellAmount}</p>
      <input type="range"  bind:value={buySellAmount} min='0' max='{buying ? cash/cookiePrice:boxesOwned}' class="big-slider" id="myRange">
      <p>your cash: ${cash}</p>
      <p>after: ${cashAfter}</p>
      <button on:click={buying ? buyCookie():sellCookie()}>{buying ? 'Buy em':'Sell em'}</button>
      <button on:click={()=>hidden = true}>Exit</button>
     </div>
    </div>
</main>

<script>
export let windowTitle;
export let windowIcon;
export let cookiePrice;
export let cash;
 $:cashAfter = buying? cash - cookiePrice * buySellAmount:cash + cookiePrice * buySellAmount;
export let boxesOwned;


export let buySellAmount = 0;

export let buying = true;
export let hidden = false;

export function buyCookie(){
  cash = cash - cookiePrice * buySellAmount;
  boxesOwned = boxesOwned + buySellAmount;
  resetBuySellAmount();
};
export function sellCookie(){
  cash = cash + cookiePrice * buySellAmount;
  boxesOwned = boxesOwned - buySellAmount;
  resetBuySellAmount();
};

export function switchMarketState(){
  if(buying){
    buying = false;
  }
  else{
    buying = true;
  }
  return buySellAmount = 0;
};
function resetBuySellAmount(){
  return buySellAmount = 0;
};

</script>

<style>

.market-container{
  width:calc(100% - 30px);
    display: flex;
    flex-direction: column;
    align-items:center;
    position: fixed;
    background:rgb(90, 187, 90);
    height:100%;
    z-index: 2;
    left:15px;
    top:0;
}
.hidden{
  display: none;
}
.switched{
    background:rgba(156, 123, 123,.96);
}

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch .custom { 
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 6px;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

.custom:checked + .slider {
  background-color: #2196F3;
}

.custom:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

.custom:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}


.big-slider {
  -webkit-appearance: none;
  width: 100%;
  height: 5px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.big-slider:hover {
  opacity: 1;
}

.big-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  background: #4CAF50;
  cursor: pointer;
}

.big-slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  background: #4CAF50;
  cursor: pointer;
}


</style>

