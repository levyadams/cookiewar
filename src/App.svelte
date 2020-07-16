<script>
	import GameManager from './modules/gameManager.svelte';
	import Time from './modules/time.svelte';

</script>

<main>
<Time />
<GameManager />

</main>

<style>
:global(html) {
    background: rgb(77, 128, 43);
  }
:global(button){
    background:rgb(2, 167, 2);
    border:none;
	color:rgb(255, 255, 255);
	border-radius: 10px;
	width:100%;
}
:global(h2){
	margin-bottom:0;
	padding-bottom:0;

}
	main {
		text-align: center;
		padding: 0 15px 15px 15px;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	@font-face {
  font-family: 'icomoon';
  src:  url('../fonts/icomoon.eot?6pcrul');
  src:  url('../fonts/icomoon.eot?6pcrul#iefix') format('embedded-opentype'),
    url('../fonts/icomoon.ttf?6pcrul') format('truetype'),
    url('../fonts/icomoon.woff?6pcrul') format('woff'),
    url('../fonts/icomoon.svg?6pcrul#icomoon') format('svg');
  font-weight: normal;
  font-style: normal;
  font-display: block;
}

:global([class^="icon-"], [class*=" icon-"]) {
  /* use !important to prevent issues with browser extensions that change fonts */
  font-family: 'icomoon' !important;
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;

  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
:global(.icon-droplet:before ){
  content: "\e90b";

}
:global(.icon-spinner5:before ){
  content: "\e97e";

}
:global(.icon-database:before ){
  content: "\e964";

}

</style>