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

	.idea-container {
		margin: 2rem 0 3rem;
	}

	.idea-form,
	.idea {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		max-width: 29.5rem;
	}

	.form-input-container,
	.form-textarea-container {
		width: 100%;
	}

	.form-input-container span,
	.form-textarea-container span {
		font-size: 0.85rem;
	}

	.form-input,
	.form-textarea {
		border-radius: 0.3rem;
		margin-bottom: 1rem;
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

	.idea-list {
		padding: 0;
	}

	.idea {
		border: 1px solid black;
		border-radius: 0.3rem;
		margin-bottom: 1rem;
		text-decoration: none;
	}

	.content {
		margin-bottom: 1rem;
	}

	.quality-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-bottom: 0.5rem;
		width: 100%;
		max-width: 7rem;
	}

	.quality-button {
		font-size: 1.25rem;
		font-weight: 800;
		margin: 0.5rem;
		padding: 0.25rem 0.5rem;
	}

	.downvote {
		background: #8d8ff8;
    padding: 0.25rem 0.64rem;
	}

	.upvote {
		background: #f84201;
	}

	.disabled {
		background: #f4f4f4;
	}

	.delete-idea-button {
		margin-bottom: 1rem;
	}

</style>

<div class="idea-container container">
	<form on:submit|preventDefault={addIdea} class="idea-form">
		<div class="form-input-container">
			<span>Idea</span>
			<input class="form-input" />
		</div>
		<div class="form-textarea-container">
			<span>Description</span>
			<textarea class="form-textarea" />
		</div>
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
						class="{quality === 'meh' ? 'disabled quality-button downvote' : 'quality-button downvote'}"
					>
							-
					</button>
					<button
						on:click={() => increaseQuality(index)}
						disabled="{quality === 'mega dope'}"
						class="{quality === 'mega dope' ? 'disabled quality-button' : 'quality-button upvote'}"
					>
						+
					</button>
				</div>
			</div>
			<button
				on:click={() => removeIdea(id)}
				class="delete-idea-button"
			>
				Delete Idea
			</button>
		</li>
	{/each}
</ul>
