<script>
	import SparkMD5 from 'spark-md5';
	import { fade,fly } from 'svelte/transition';

	let okpass=false, pass, good = true;

	let checkPwd = () => {
		good = SparkMD5.hash(pass) === "1074933385f0940596363e3692459911";
		okpass = true;
	}

</script>

<main>
	<div class="flexman">
		<img src='logo-servair.png' alt="logo servair" class="logo">
	</div>
	{#if !okpass}
	<div class="flexman">
			<h2 style="padding-top:3vh;">Voeux d'Alexis Frantz</h2>
			<p>Rendez-vous sur cette page, le mardi 25 Janvier, à 14H00</p>
	</div>
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
	<div class="container-iframe vid" in:fade={{delay:1000}}>
		<!-- svelte-ignore a11y-missing-attribute -->
		<iframe 
		src="https://player.castr.com/live_40ad681076e411ec9415d32a788dbfab" 
		width="590" 
		height="431" 
		frameborder="0" 
		scrolling="no" 
		allow="autoplay" 
		allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>
	</div>
	{/if}
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

	.container-iframe {
		position: relative;
		overflow: hidden;
		width: 100%;
		padding-top: 56.25%; /* 16:9 Aspect Ratio (divide 9 by 16 = 0.5625) */
	}

	iframe {
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		width: 100%;
		height: 100%;
	}

</style>