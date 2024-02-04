<script>
	import { navigate } from 'svelte-routing'
	import accentColor from '../store/store'

	let aColor
	accentColor.subscribe(value => (aColor = value))

	function toHome(e) {
		e.preventDefault()
		accentColor.set('#FF4655')
		navigate('/', { replace: true })
	}
</script>

<header
	class="px-8 py-4 flex items-center justify-center fixed w-full bg-[#0F1923] bg-opacity-70 backdrop-blur-md z-30"
>
	<div class="flex items-center justify-between w-full">
		<a
			href="/"
			on:click={toHome}
			class="font-bold text-lg flex items-center my-hover hover:scale-[1.05]"
			style="color: {aColor}"
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				class="h-7 w-7 mr-3"
				style="fill: {aColor}"
				viewBox="0 0 100 100"
			>
				<path
					d="M99.25 48.66V10.28c0-.59-.75-.86-1.12-.39l-41.92 52.4a.627.627 0 00.49 1.02h30.29c.82 0 1.59-.37 2.1-1.01l9.57-11.96c.38-.48.59-1.07.59-1.68zM1.17 50.34L32.66 89.7c.51.64 1.28 1.01 2.1 1.01h30.29c.53 0 .82-.61.49-1.02L1.7 9.89c-.37-.46-1.12-.2-1.12.39v38.38c0 .61.21 1.2.59 1.68z"
				></path>
			</svg>
			<div>Valorant</div>
		</a>
		<div>
			<a
				target="_blank"
				href="https://vk.com/l3_dima"
				class="text-gray-400 text-sm hover:text-white"
			>
				@ Babich Dmitriy, 2024
			</a>
		</div>
	</div>
</header>

<style>
	.my-hover {
		transition: all 0.25s cubic-bezier(0.65, 0, 0.35, 1);
	}
</style>
