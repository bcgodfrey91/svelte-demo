<script>
	const lsIdeas = JSON.parse(localStorage.getItem('ideas'));
	const setLocalIdeas = () => localStorage.setItem('ideas', JSON.stringify(ideas));
	let ideas = lsIdeas ? lsIdeas : [];
	let title = '';
	let content = '';
	let search = ''

	const addIdea = (e) => {
		ideas = [
			...ideas,
			{
				id: Date.now(),
				title: title,
				content: content,
				quality: 'meh'
			}
		];
		title = '';
		content = '';
		setLocalIdeas();
	};

	const removeIdea = (id) => {
		ideas = ideas.filter((idea) => id !== idea.id);
		setLocalIdeas();
	}

	const increaseQuality = (identifier) => {
		ideas[identifier].quality = ideas[identifier].quality === 'meh' ? 'cool I guess' : 'mega dope';
		setLocalIdeas();
	}

	const decreaseQuality = (identifier) => {
		ideas[identifier].quality = ideas[identifier].quality === 'mega dope' ? 'cool I guess' : 'meh';
		setLocalIdeas();
	}

	$: filtered = search.trim().length
				? ideas.filter(
						idea => idea.title.toLowerCase().includes(search.toLowerCase())
						|| idea.content.toLowerCase().includes(search.toLowerCase())
					)
				: ideas;

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
		margin: 2rem 0 2rem;
	}

	.idea-form,
	.idea,
	.search-input-container {
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
	.form-textarea,
	.search-input {
		border-radius: 0.3rem;
		margin-bottom: 1rem;
		width: 100%;
	}

	.form-input,
	.search-input {
		font-size: 1.5rem;
		height: 3rem;
	}

	.form-textarea {
		height: 7rem;
		resize: none;
	}

	.search-input-container {
		margin-bottom: 2rem;
	}

	.hidden {
		display: none;
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

	.quality-button:hover {
		cursor: pointer;
	}

	.downvote {
		background: #8d8ff8;
    padding: 0.25rem 0.64rem;
	}

	.upvote {
		background: #f84201;
	}

	.disabled,
	.post-disabled {
		background: #f4f4f4;
	}

	.disabled:hover,
	.post-disabled:hover {
		cursor: initial;
	}

	.post-idea-button,
	.delete-idea-button,
	.post-disabled {
		border-radius: 0.3rem;
		padding: 0.75rem 0;
		width: 100%;
		max-width: 6.44rem;
	}

	.delete-idea-button {
		margin-bottom: 1rem;
	}

	.post-idea-button:hover {
		background: #37d2a7;
		cursor: pointer;
	}

	.delete-idea-button:hover {
		background: #ff0000;
		cursor: pointer;
	}

</style>

<div class="idea-container container">
	<form on:submit|preventDefault={addIdea} class="idea-form">
		<div class="form-input-container">
			<label for="title">Idea</label>
			<input
				bind:value={title}
				class="form-input"
			/>
		</div>
		<div class="form-textarea-container">
			<label for="content">Description</label>
			<textarea
				bind:value={content}
				class="form-textarea"
			/>
		</div>
		<button
			disabled="{!title.length || !content.length}"
			class="{title.length && content.length ? 'post-idea-button' : 'post-disabled'}"
		>
			Post Idea
		</button>
	</form>
</div>

<div class="{ideas.length ? 'search-input-container' : 'hidden'}">
	<input
		bind:value={search}
		class="search-input"
		placeholder="Search Ideas"
	/>
</div>

<ul class="idea-list container">
	{#each filtered as {id, title, content, quality}, index (id)}
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
