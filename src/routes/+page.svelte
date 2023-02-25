<script lang="ts">
	import Katex from 'svelte-katex';

	let x = '';
	let y = '';

	let oper: '' | '+' | '-' | '*' | '/' | '^' = '';
	let KatexString = '';

	function setString() {
		switch (oper) {
			case '+':
				KatexString = `${x} + ${y}`;
				break;
			case '-':
				KatexString = `${x} - ${y}`;
				break;
			case '*':
				KatexString = `${x} \\times ${y}`;
				break;
			case '/':
				KatexString = `\\frac{${x}}{${y}}`;
				break;
			case '^':
				KatexString = `${x}^{${y}}`;
				break;
			default:
				KatexString = `${x}  ${y}`;
				break;
		}
	}
</script>

<div class="bg-gray-800 p-4 rounded-lg my-3 mx-5">
	<div class="text-white mx-7 my-5 text-xl">Kalkulator różniczki zupełnej</div>
	<div class="flex flex-row">
		<input
			class="bg-gray-700 text-white w-1/2 p-2 rounded-lg mx-7"
			type="text"
			bind:value={x}
			on:input={setString}
			placeholder="x"
		/>
		<select
			class="bg-gray-900 text-white w-1/4 p-2 rounded-lg"
			bind:value={oper}
			on:change={setString}
		>
			<option value="">Wybierz</option>
			<option value="+">+</option>
			<option value="-">-</option>
			<option value="*">*</option>
			<option value="/">/</option>
			<option value="^">^</option>
		</select>
		<input
			class="bg-gray-700 text-white w-1/2 p-2 rounded-lg mx-7"
			type="text"
			bind:value={y}
			on:input={setString}
			placeholder="y"
		/>
	</div>
	<div class="flex flex-row mt-10 justify-center items-center text-2xl">
		<span class="mx-1">Wyrażenie:</span><Katex>{KatexString}</Katex>
	</div>
</div>

<!-- solver tab rounded-->
<div class="bg-gray-800 p-4 rounded-lg my-3 mx-5">
	<Katex>\varDelta f \approx df</Katex><br />
	<Katex>f(x_0 + dx, y_0+dy) - f(x_0, y_0) \approx f_x(x_0, y_0)dx + f_y(x_0,y_0)dy</Katex><br />
	<Katex>f(x_0 + dx, y_0+dy) \approx f(x_0, y_0) + f_x(x_0, y_0)dx + f_y(x_0,y_0)dy</Katex><br />
</div>
