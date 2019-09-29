<script>
	let ideas = [];
	let count = 0;

	const addIdea = (e) => {
		ideas = [
			...ideas,
			{
				title: e.target[0].value,
				content: e.target[1].value,
				id: count
			}
		];
		count++;
	};

	const removeIdea = (i) => {
		ideas = ideas.filter((idea, index) => i !== index);
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
	{#each ideas as idea, i (idea.id)}
		<li>
			<h1>{idea.title}</h1>
			<span>{idea.content}</span>
			<button on:click={() => removeIdea(i)}>Delete Idea</button>
		</li>
	{/each}
</ul>
