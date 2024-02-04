<script>
	export let nameAgent
	import accentColor from '../store/store'

	import { Agents } from '../constansts/Agents.data.js'
	import { Role } from '../constansts/Role.data'
	let agent = Agents.find(agent => agent.name.toLocaleLowerCase() === nameAgent)
	accentColor.set(agent.color)
	let aColor
	accentColor.subscribe(value => (aColor = value))

	let imgAgent
	// parallax
	// document.addEventListener('mousemove', e => {
	// 	imgAgent.style.transform = `translate(-${
	// 		(e.clientX / window.innerWidth) * 10
	// 	}px, -${(e.clientY / window.innerHeight) * 10}px)`
	// })

	// parallax 3d
	document.addEventListener('mousemove', e => {
		imgAgent.style.transform = `rotateX(${
			(e.clientY - window.innerHeight / 2) * -0.1
		}deg) rotateY(${(e.clientX - window.innerWidth / 2) * -0.05}deg)`
	})

	let activeSkill = 1
</script>

<div class="flex">
	<div
		id="mask"
		class="fixed w-[100%] h-[100%] top-0 left-0 flex justify-center bg-cover bg-no-repeat my-mask"
		style="background-image: url({agent.bg}); aspect-ratio: 16 / 9; background-position: top left;"
	></div>
	<section
		class="flex mb-10 w-[80vw] text-white border border-1 border-[#ffffff3b] rounded-xl overflow-hidden flex-row-reverse bg-[#0F1923] bg-opacity-35 z-10"
	>
		<div class="flex items-center justify-center w-3/5">
			<img
				bind:this={imgAgent}
				class="h-[85vh] opacity-85 parallax-3d"
				src={agent.imgBig}
				alt="agent"
				style="filter: drop-shadow(0.25rem 0.25rem 0.25rem #0F1923) drop-shadow(0 0 0.75rem {agent.color})"
			/>
		</div>
		<div
			class="flex flex-col w-2/5 gap-3 items-start pt-14 pb-10 pl-7 pr-10 backdrop-blur-md rounded-xl"
		>
			<div
				class="text-3xl font-extrabold tracking-widest"
				style="color: #fff; text-shadow: 2px 2px 10px {aColor}, -2px -2px 10px {aColor}"
			>
				{agent.name.toLocaleUpperCase()}
			</div>
			<div>
				<div class="font-bold text-gray-500">// ROLE</div>
				<div class="text-3xl flex gap-4 font-bold items-center">
					<span>
						{agent.role.toLocaleUpperCase()}
					</span>
					<span class="flex items-center justify-center w-8 h-8">
						<img src={Role[agent.role]} alt="img_role" />
					</span>
				</div>
			</div>
			<div>
				<div class="font-bold text-gray-500">// BIOGRAPHY</div>
				<div class="text-md">{agent.biography}</div>
			</div>
			<div>
				<div class="font-bold text-gray-500 mb-3">// SPECIAL ABILITIES</div>
				<div class="flex gap-3 mb-3">
					{#each agent.skills as item}
						<button
							on:click={() => (activeSkill = item.id)}
							class="w-12 h-12 p-2 border border-1 border-white rounded-xl opacity-30 hover:opacity-100 btn-skill"
							style="--color:{agent.color};"
							class:active={activeSkill === item.id}
						>
							<img src={item.image} alt="skill" />
						</button>
					{/each}
				</div>
				<div class="flex flex-col gap-1">
					<h4 class="font-bold">{agent.skills[activeSkill - 1].name}</h4>
					<p class="text-md leading-5">{agent.skills[activeSkill - 1].info}</p>
				</div>
			</div>
		</div>
	</section>
</div>

<style>
	.my-mask {
		-webkit-mask: linear-gradient(
			90deg,
			rgba(255, 255, 255, 0) 20%,
			rgba(255, 255, 255, 0.5) 60%,
			rgba(255, 255, 255, 1) 100%
		);
	}

	/* .my-hover {
		transition: all 0.1s ease;
	} */

	.parallax-3d {
		transform-style: preserve-3d;
		will-change: transform;
		transition: transform 1.5s cubic-bezier(0.05, 0.5, 0, 1);
	}

	.btn-skill {
		transition: all 0.25s cubic-bezier(0.65, 0, 0.35, 1);
	}

	.btn-skill:hover {
		box-shadow: 4px 4px 0 -1px var(--color);
		transform: translate(-4px, -4px);
	}

	.btn-skill.active {
		box-shadow: 4px 4px 0 -1px var(--color);
		transform: translate(-4px, -4px);
		opacity: 1;
	}
</style>
