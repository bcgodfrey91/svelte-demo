<script>
	let ideas = [];

	const addIdea = (e) => {
		ideas = [
			...ideas,
			{
				title: e.target[0].value,
				content: e.target[1].value,
				id: Date.now()
			}
		];
	};

	const removeIdea = (i) => {
		ideas = ideas.filter((idea) => i !== idea.id);
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
	{#each ideas as {title, content, id}}
		<li>
			<h1>{title}</h1>
			<span>{content}</span>
			<div>{id}</div>
			<button on:click={() => removeIdea(id)}>Delete Idea</button>
		</li>
	{/each}
</ul>
