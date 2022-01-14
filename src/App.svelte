<script>
	//https://www.youtube.com/watch?v=QdStKZkNWm4
	import Plyr from 'plyr';
	import SparkMD5 from 'spark-md5';
	import { fade,fly } from 'svelte/transition';

	let player, okpass, pass, good = true;
	//const hexHash = SparkMD5.hash('@voeux2022@');
	
	document.body.addEventListener("copy", function(e){
			console.log("chouette");
				e.preventDefault();
				e.stopPropagation();
		});
				document.body.addEventListener("cut", function(e){
				e.preventDefault();
				e.stopPropagation();
		});

	let checkPwd = () => {
		good = SparkMD5.hash(pass) === "35038d9b000045edd73fd3134fa45c4a";
		okpass = true;
		setTimeout(() => loadPlay(), 500);
	}

	let loadPlay = async()=> {
		player = new Plyr('#player', {autoplay : true, controls : ['current-time', 'volume', 'mute'],  youtube :
			{ rel: 0, modestbranding: 1, controls : 2, autplay : 1 }
		});
		player.play();
		//[...document.querySelectorAll('ytp-button')].forEach(el => { el.style.opacity = 0 });
		
	};

</script>

<main>
	<div class="flexman">
		<img src='logo-servair.png' alt="logo servair" class="logo">
		<h2 style="padding-top:3vh;">Lorem ipsum</h2>
		<p>Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore</p>
	</div>

	{#if !okpass}
	<div class="container" out:fly>
		<div class="row">
		  <div class="column"></div>
		  <div class="column">
			<form on:submit|preventDefault={checkPwd}>
				<fieldset>
				  <label for="nameField">Mot de passe</label>
				  <input bind:value={pass} type="password" placeholder="Veuillez saisir le mot de pass du live" id="pass">
				  <div class="message" style="margin-bottom:-1em;" class:invisible={good || (pass !== undefined && !pass.length)}>
					<label style="color:red;" class="label-inline" for="confirmField">Mot de passe incorrect</label>
				  </div>
				  <input class="button-primary" type="submit" value="OK">
				</fieldset>
			  </form>		  
		  </div>
		  <div class="column"></div>
		</div>	  
	  </div>
	{:else}
	<div class="container vid" in:fade={{delay:1000}}>
		<!---->
		<!-- <iframe width="560" height="315" src="https://www.youtube.com/embed/QdStKZkNWm4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> -->
		<div id="player" data-plyr-provider="youtube" data-plyr-embed-id="0tgVXTNiQOM"></div>
	</div>
	{/if}
	<!-- Plyr resources and browser polyfills are specified in the pen settings -->
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
		.flexman {
			padding : 0vh 35%;
		}
	}
	.label-inline {
		position: relative;
    	top: -1em;
	}
	.invisible {
		opacity: 0;
	}
	.logo {
		max-width:300px;
	}
	form {
		margin-top:1.5rem;
	}
	:global(.ytp-button) {
		opacity: 0;
	}
	.vid {
		clip-path: inset(100px 0 0 0px);
	}


</style>