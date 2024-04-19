<script>
	import { page } from '$app/stores';
	import logo from '$lib/images/logo.svg';
</script>

<header>
	<div id="logo">
		<a href="/">
			<img src={logo} alt="Coffee Blog" />
		</a>
	</div>

	<nav >
		<svg id="svg-line" viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 C1.5,3 2,3 2,3 L2,0 Z" />
		</svg>
		<ul>
			<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
				<a href="/">Home</a>
			</li>
			<li aria-current={$page.url.pathname === '/login' ? 'page' : undefined}>
				<a href="/login">Login</a>
			</li>
		</ul>
	</nav>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
		background: #444444;
		view-transition-name: header;
	}

	#logo a {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100%;
	}

	#logo img {
		margin-left: 3vw;
		height: 2.2em;
		object-fit: contain;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: var(--color-bg-0);
		transition: background-color .3s linear;
		view-transition-name: navbar;
	}

	#svg-line {
		width: 2em;
		height: 3em;
		display: block;
	}

	path {
		fill: var(--background);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	li[aria-current='page']::before {
		--width: 30px;
		--height: 3px;
		content: '';
		width: var(--width);
		height: var(--height);
		position: absolute;
		top: 0;
		left: calc(50% - var(--width) / 2);
		background-color: var(--color-theme-1);
		view-transition-name: indicator;
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 2em;
		color: var(--color-text);
		font-weight: 700;
		font-size: .8rem;
		text-transform: uppercase;
		letter-spacing: .2em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
