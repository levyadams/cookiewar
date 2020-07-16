<main>
    <div class="locations-container">
    {#each locations as location}
        <p>{location.name}</p>
    {/each}
    </div>
</main>
<script>
export let locations;
</script>
<style>
.locations-container{
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
</style>