<script>
	import { Agents } from '../constansts/Agents.data.js'
</script>

<aside
	class="flex items-center justify-center fixed right-0 pr-4 top-[50%] translate-y-[-50%] z-30"
>
	<nav>
		<ul class="flex flex-col">
			{#each Agents as agent, index}
				<li>
					<a
						href={agent.href}
						class="border-3 border-[#FF4655] w-10 h-10 flex items-center text-[#FF4655] justify-center rounded-md hover:bg-[#FF4655] bg-[#FF4655] mb-2 overflow-hidden my-hover hover:scale-[1.1]"
					>
						<img src={agent.imgSmall} alt="small_image" />
					</a>
				</li>
			{/each}
		</ul>
	</nav>
</aside>

<style>
	.my-hover {
		transition: all 0.25s cubic-bezier(0.65, 0, 0.35, 1);
	}
</style>
