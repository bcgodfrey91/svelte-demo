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
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		margin: 0 2.5vw;
		width: 100%;
	}

	.idea-form {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		max-width: 29.5rem;
	}

	.form-input,
	.form-textarea {
		border-radius: .3rem;
		width: 100%;
	}

	.form-input {
		font-size: 1.5rem;
		height: 3rem;
	}

	.form-textarea {
		height: 7rem;
		resize: none;
	}

</style>

<div class="container">
	<form on:submit|preventDefault={addIdea} class="idea-form">
		<input class="form-input" />
		<textarea class="form-textarea" />
		<button class="post-idea">Post Idea</button>
	</form>
</div>

<ul class="idea-list container">
	{#each ideas as {id, title, content, quality}, index (id)}
		<li class="idea">
			<h1 class="title">
				{title}
			</h1>
			<span class="content">
				{content}
			</span>
			<div class="quality-container">
				<span class="quality">
					{quality}
				</span>
				<div class="button-container">
					<button
						on:click={() => decreaseQuality(index)}
						disabled="{quality === 'meh'}"
						class="{quality === 'meh' ? 'disabled quality-button' : 'quality-button'}"
					>
							-
					</button>
					<button
						on:click={() => increaseQuality(index)}
						disabled="{quality === 'mega dope'}"
						class="{quality === 'mega dope' ? 'disabled quality-button' : 'quality-button'}"
					>
						+
					</button>
				</div>
			</div>
			<button
				on:click={() => removeIdea(id)}
				class="delete-idea"
			>
				Delete Idea
			</button>
		</li>
	{/each}
</ul>
