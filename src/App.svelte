<script>
	let ideas = [];
	const addIdea = (e) => {
		ideas = [
			...ideas,
			{
				title: e.target[0].value,
				content: e.target[1].value
			}
		]
	}
</script>

<style>
</style>

<form on:submit|preventDefault={addIdea}>
	<input />
	<textarea />
	<button>Post Idea</button>
</form>

<ul>
	{#each ideas as idea}
		<li>
			<h1>{idea.title}</h1>
			<span>{idea.content}</span>
		</li>
	{/each}
</ul>
