<main>
    <button on:click={()=> assetWindowHidden ? assetWindowHidden = false:assetWindowHidden = true}><div class="icon-book"></div></button>
    <div class:hidden={assetWindowHidden} class="asset-container">
        <button on:click={()=>paybackLoan()}>Pay back loan</button>
        <button class:hidden={currentLocation.safehouse} on:click={()=>buySafehouseAtLocation()}>buy safehouse ($2000)</button>
        <button  on:click={()=>assetWindowHidden = true}>back</button>
    </div>
</main>

<script>
import AssetManager from './assetManager.svelte';

export let currentLocation;

finish making the safehouse window pop up

export let assetWindowHidden = true;

export let loanPaid = false;

export let cash = 0;

let paybackLoan =()=>{
if(cash>=5000){
    cash = cash - 5000;
    loanPaid = true;
    alert("Ma': 'great work..Good luck out there, sweetheart!'");
}
else{
    alert("Ma':'You dont have enough cash, sweetheart!'");
}
};

let buySafehouseAtLocation =()=>{
    if(!currentLocation.safehouse){
        if(cash>=currentLocation.safehousePrice){
            cash = cash - currentLocation.safehousePrice;
            currentLocation.safehouse = true;
            alert('Thanks! Here are the keys!');
        }
    }
};

</script>

<style>
.asset-container{
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
    display:none;
}
</style>