<script>
	export let segment;
	import { goto, stores } from '@sapper/app';
	import {post} from 'utils.js';
	const { page, session } = stores();

	async function logout(){
		await post('auth/logout');
		$session.token=null;
		goto('/');
	}
</script>

<style>
	nav {
		border-bottom: 1px solid rgba(255,62,0,0.1);
		font-weight: 300;
		padding: 0 1em;
	}

	ul {
		margin: 0;
		padding: 0;
	}

	/* clearfix */
	ul::after {
		content: '';
		display: block;
		clear: both;
	}

	li {
		display: block;
		float: left;
	}

	[aria-current] {
		position: relative;
		display: inline-block;
	}

	[aria-current]::after {
		position: absolute;
		content: '';
		width: calc(100% - 1em);
		height: 2px;
		background-color: rgb(255,62,0);
		display: block;
		bottom: -1px;
	}

	a {
		text-decoration: none;
		padding: 1em 0.5em;
		display: block;
	}
</style>
{JSON.stringify($session)}
<nav>
	<ul>
		{#if $session.token}
			<li><a aria-current="{segment === 'logout' ? 'page' : undefined}" href="{logout}" on:click|preventDefault={logout}>log out</a></li>
		{:else}
			<li><a aria-current="{segment === 'register' ? 'page' : undefined}" href="register">register</a></li>
			<li><a aria-current="{segment === 'login' ? 'page' : undefined}" href="login">log in</a></li>
		{/if}

		<!-- for the blog link, we're using rel=prefetch so that Sapper prefetches
		     the blog data when we hover over the link or tap it on a touchscreen -->
	</ul>
</nav>