<main>
    <div class:hidden={infoWindowHidden} class="info-container">
        <p class:hidden={!startGame}>{firstMessage}</p>
        <p class:hidden={!endGame}>{finishMessage}</p>
        <button on:click={()=>startingMessageFunction()}>OK!</button>
    </div>
</main>

<script>
    export let currentDay = 0;
    export let cash;
    export let firstMessage = "This game...and really this entire site, are a WIP and the only reason you are reading this is because I like testing on live instances."
    export let finishMessage = `Game over! Your score was ${cash}`;
    export let startGame = true;
    export let endGame = false;
    export let infoWindowHidden = false;

    $:{
        if(currentDay === 31){
            infoWindowHidden = false;

            endGame = true;
        }
    }

     let startingMessageFunction=()=>{
         if(startGame){

             startGame = false;
         infoWindowHidden = true;
         return;
         }
         else{
             location.reload();
         }
    };

</script>

<style>

.info-container{
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