<script>
	import { Route, Router } from 'svelte-routing'
	import { Agents } from './constansts/Agents.data'
	import Aside from './lib/ASide.svelte'
	import Header from './lib/Header.svelte'
	import Agent from './routes/Agent.svelte'
	import accentColor from './store/store'

	let aColor
	accentColor.subscribe(value => (aColor = value))

	function getImage() {
		console.log(aColor)
		let agent = Agents.find(agent => agent.color === aColor)
		if (agent) return agent.bg
		else console.log(agent)
	}

	let bg = getImage()
	export let url = ''
</script>

<Router {url}>
	<Header />
	<Aside />
	<main class="flex h-full flex-col items-center pt-20">
		<Route path="/agent/:name" let:params>
			<Agent nameAgent={params.name} />
		</Route>
		<Route path="/">
			<h1 class="mb-4 text-4xl font-bold text-gray-500">AGENTS</h1>
			<!-- <div class="w-[90vw] flex flex-col gap-2">
				{#each Agents as agent}
					<a
						href={agent.href}
						class="font-bold text-[#FF4655] link flex align-top"
					>
						<span class="text-2xl mt-4 mr-4">{agent.id}.</span>
						<span class="text-8xl">{agent.name}</span>
					</a>
				{/each}
			</div> -->
			<div class="flex h-[100%] items-center justify-center">
				<div class="h-[100px] w-[700px] overflow-hidden">
					<ul class="scroll">
						{#each Agents as agent}
							<li>
								<a
									href={agent.href}
									class="font-bold text-[#FF4655] link flex align-top"
								>
									<span class="text-2xl mt-4 mr-4">{agent.id}.</span>
									<span class="text-8xl">{agent.name}</span>
									<div class="item-link">
										<svg
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											class="ml-1 h-12 w-12"
											style="fill: {aColor}"
											viewBox="0 0 100 100"
										>
											<path
												d="M99.25 48.66V10.28c0-.59-.75-.86-1.12-.39l-41.92 52.4a.627.627 0 00.49 1.02h30.29c.82 0 1.59-.37 2.1-1.01l9.57-11.96c.38-.48.59-1.07.59-1.68zM1.17 50.34L32.66 89.7c.51.64 1.28 1.01 2.1 1.01h30.29c.53 0 .82-.61.49-1.02L1.7 9.89c-.37-.46-1.12-.2-1.12.39v38.38c0 .61.21 1.2.59 1.68z"
											></path>
										</svg>
									</div>
								</a>
							</li>
						{/each}
					</ul>
				</div>
			</div>
		</Route>
	</main>
</Router>

<style>
	.link {
		cursor: pointer;
		vertical-align: top;
	}

	.link span:last-child {
		transition: all 0.25s;
	}

	.link:hover span:last-child {
		transform: translateX(10px);
	}

	.link:hover .item-link {
		opacity: 1;
		transform: rotate(90deg) translateY(0);
	}

	.scroll {
		animation: flip 10s ease-in-out infinite;
	}

	@keyframes flip {
		0%,
		33% {
			transform: translate(0px, -200px);
		}
		33%,
		66% {
			transform: translate(0px, -100px);
		}
		66%,
		100% {
			transform: translate(0px, 0px);
		}
		100%,
		0% {
			transform: translate(0px, -200px);
		}
	}

	.item-link {
		transition: all 0.25s;
		opacity: 0;
		transform: rotate(90deg) translateY(-200px);
	}
</style>
