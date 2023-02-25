<script lang="ts">
	import Katex from 'svelte-katex';

	let x = '';
	let array: string[] = [];
</script>

<p class="my-3 mx-8">
	<a
		class="text-xl text-cyan-50"
		href="https://katex.org/docs/supported.html"
		target="_blank"
		rel="noreferrer noopener">Dokumentacja</a
	>
</p>
<!-- Teaxt area in dark mode to input x + Katex ouptut belowe-->
<input
	class="bg-gray-700 text-white w-1/2 p-2 rounded-lg mx-7"
	type="text"
	bind:value={x}
	placeholder="x"
/>

<button
	class="bg-gray-600 text-white rounded-lg"
	on:click={() => {
		array = [...array, x];
	}}
>
	Dodaj
</button>

<!-- save to txt button-->
<button
	class="bg-gray-600 text-white mx-2 rounded-lg"
	on:click={() => {
		let text = '';
		array.forEach((item) => {
			text += item + '\n';
		});
		const element = document.createElement('a');
		const file = new Blob([text], { type: 'text/plain' });
		element.href = URL.createObjectURL(file);
		element.download = 'text.txt';
		document.body.appendChild(element); // Required for this to work in FireFox
		element.click();
	}}
>
	Zapisz do pliku
</button><br />

<ul class="mx-8">
	{#each array as item}
		<li class="my-2"><Katex>{item}</Katex> &nbsp;&nbsp;&nbsp;&nbsp; {item}</li>
	{/each}
</ul>
