<main>
    <button class:hidden={loanPaid} on:click={()=> paybackLoan()}>Pay back loan!</button>
</main>
<script>
    export let cash;

    export let loanPaid = false;
    let paybackLoan =()=>{
        if(cash>=5000){
            cash = cash - 5000;
            loanPaid = true;
            alert("Ma': 'great work. Good luck out there, sweetheart!'");
        }
        else{
            alert("Ma':'You dont have enough cash, sweetheart!'");
        }
    };
</script>

<style>
.hidden{
    display:none;
}
</style>