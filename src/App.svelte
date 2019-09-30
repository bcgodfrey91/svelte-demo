<script>
	let ideas = [];

	const addIdea = (e) => {
		ideas = [
			...ideas,
			{
				id: Date.now(),
				title: e.target[0].value,
				content: e.target[1].value,
				quality: 'meh'
			}
		];
	};

	const removeIdea = (id) => {
		ideas = ideas.filter((idea) => id !== idea.id);
	}

	const increaseQuality = (identifier) => {
		ideas[identifier].quality = ideas[identifier].quality === 'meh' ? 'cool I guess' : 'mega dope';
	}

	const decreaseQuality = (identifier) => {
		ideas[identifier].quality = ideas[identifier].quality === 'mega dope' ? 'cool I guess' : 'meh';
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
	{#each ideas as {id, title, content, quality}, index (id)}
		<li>
			<h1>{title}</h1>
			<span>{content}</span>
			<div>
				{quality}
				<button
					on:click={() => decreaseQuality(index)}
					disabled="{quality === 'meh'}"
				>
						-
				</button>
				<button
					on:click={() => increaseQuality(index)}
					disabled="{quality === 'mega dope'}"
				>
					+
				</button>
			</div>
			<button on:click={() => removeIdea(id)}>Delete Idea</button>
		</li>
	{/each}
</ul>
