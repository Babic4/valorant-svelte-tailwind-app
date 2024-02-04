<script>
	export let agent
</script>

<a href="#">
	<div
		class="flex content-stretch flex-col rounded-xl border border-1 border-[#ffffff3b] overflow-hidden bg-[#0F1923] h-[450px]"
	>
		<div class="h-2/3 overflow-hidden">
			<img src={agent.imgBig} alt="agent" />
		</div>
		<div
			class="flex items-center justify-center text-3xl font-extrabold tracking-widest"
			style="color: {agent.color}; text-shadow: 2px 2px 10px {agent.color}, -2px -2px 10px {agent.color}"
		>
			{agent.name.toLocaleUpperCase()}
		</div>
	</div>
</a>

<style>
</style>
