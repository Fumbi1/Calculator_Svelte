<script>
	const Signs = ['+', '-', '*', '/', '**', '%', '.'];
	const Numbers = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0'];
	let boolean = false;
	let inputValue = 0;
	let answerValue = 0;

	function handleClick(key) {
		if (inputValue != 0) {
			inputValue += key;
		} else {
			inputValue = key;
		}
		disableButton();
	}

	function calc() {
		const lastChar = inputValue.trim().slice(-1);
		if (Signs.includes(lastChar)) {
			answerValue = 'Input a correct Expression';
		} else {
			answerValue = Function('return ' + inputValue)();
		}
	}

	function disableButton() {
		let lastChar = inputValue.trim().slice(-1);
		if (Signs.includes(lastChar)) {
			boolean = true;
		} else {
			boolean = false;
		}
		return boolean;
	}

	function clearValue() {
		inputValue = 0;
		answerValue = 0;
	}

	function deleteValue() {
		let modifiedValue = [...inputValue];
		modifiedValue.pop();
		{
			modifiedValue.length === 0 ? (inputValue = 0) : (inputValue = modifiedValue.join(''));
		}
	}
</script>

<div class="main">
	<div class="wrapper">
		<div class="input">{inputValue}</div>

		<div>
			<div class="answer">{answerValue}</div>
		</div>

		<div class="inline">
			<button class="clear" on:click={() => clearValue()}>
				<p>AC</p>
			</button>
			<button class="clear" on:click={() => deleteValue()}>
				<p>DEL</p>
			</button>
		</div>

		<div class="grid">
			<div class="flex">
				{#each Numbers as Number}
					<div>
						<button class="test" on:click={() => handleClick(Number)}>
							{Number}
						</button>
					</div>
				{/each}
			</div>

			<div class="flex2">
				{#each Signs as Sign}
					<div>
						<button class="test2" on:click={() => handleClick(Sign)} disabled={boolean}>
							{Sign}
						</button>
					</div>
				{/each}
				<button class="operate" on:click={() => calc()}>
					<p>=</p>
				</button>
			</div>
		</div>
	</div>
</div>

<style>
	.main {
		width: 100%;
		cursor: pointer;
	}

	.wrapper {
		width: 95%;
		margin-inline: auto;
	}

	.input {
		background-color: transparent;
		width: 100%;
		text-align: right;
		font-size: 2.5rem;
		color: grey;
		margin-top: 4rem;
	}

	.answer {
		margin-top: 2rem;
		width: 100%;
		text-align: right;
		font-size: 4rem;
		color: white;
	}

	.inline {
		display: flex;
		width: 100%;
		justify-content: flex-end;
		column-gap: 1rem;
		margin-top: 1rem;
	}

	.clear {
		margin-bottom: 1rem;
		width: fit-content;
		padding: 0.75rem;
		border-radius: 0.5rem;
		background-color: #9b7f5b;
	}

	.clear > p {
		color: white;
		font-size: 2rem;
	}

	.grid {
		display: flex;
		justify-content: space-between;
	}

	.flex {
		display: flex;
		flex-wrap: wrap;
		column-gap: 33%;
		row-gap: 0.5rem;
		margin-top: 3rem;
		width: 70%;
	}

	.flex2 {
		display: flex;
		flex-wrap: wrap;
		column-gap: 33%;
		row-gap: 0.5rem;
		margin-top: 3rem;
		width: 30%;
		justify-content: space-between;
	}

	.operate {
		background-color: #0096ff;
		text-align: center;
		color: white;
		width: 100%;
		padding-block: 1rem;
		margin-inline: auto;
		height: fit-content;
		border-radius: 0.5rem;
		font-size: 3rem;
		font-weight: 900;
	}

	.test {
		width: fit-content;
		padding: 1rem;
		border-radius: 0.5rem;
		background-color: #262521;
		font-size: 1.5rem;
		color: antiquewhite;
	}

	.test2 {
		width: fit-content;
		padding: 1rem;
		border-radius: 0.5rem;
		background-color: #708090;
		font-size: 1.5rem;
	}

	@media (max-width: 583px) {
		.flex {
			display: flex;
			flex-wrap: wrap;
			column-gap: 25%;
			row-gap: 0.5rem;
			margin-top: 3rem;
			width: 70%;
		}

		.flex2 {
			display: flex;
			flex-wrap: wrap;
			column-gap: 25%;
			row-gap: 0.5rem;
			margin-top: 3rem;
			width: 30%;
			justify-content: space-between;
		}
	}

	@media (max-width: 398px) {
		.flex {
			display: flex;
			flex-wrap: wrap;
			column-gap: 18%;
			row-gap: 0.5rem;
			margin-top: 3rem;
			width: 70%;
		}
	}

	@media (max-width: 388px) {
		.flex2 {
			display: flex;
			flex-wrap: wrap;
			column-gap: 33%;
			row-gap: 0.5rem;
			margin-top: 3rem;
			width: 30%;
			justify-content: flex-end;
		}
	}
</style>
