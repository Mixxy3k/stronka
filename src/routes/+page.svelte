<script lang="ts">
	import Katex from 'svelte-katex';
	import evaluatex from 'evaluatex/dist/evaluatex';

	let x = 0;
	let y = 0;
	let x0 = 0;
	let y0 = 0;
	let dx = 0;
	let dy = 0;
	let z=0;

	let oper: '' | '+' | '-' | '*' | '/' | '^' = '';
	let KatexString = '';
	let zString = 'x+y';
	let zString1=''


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
	function roundCos(){
		dx = x % 1;
		dy = y % 1;
		if (dx < 0.5) {
            x0 = Math.floor(x);
  		} else {
			x0 = Math.ceil(x);
  		}
		  if (dy < 0.5) {
            y0 = Math.floor(y);
  		} else {
			y0 = Math.ceil(y);
  		}

		dx= Number((x-x0).toFixed(2));
		dy= Number((y-y0).toFixed(2));

		
	}

	function show(){
		zString = KatexString.replace(`${x}`, `x`).replace(`${y}`, `y`);
		zString1 = zString.replace(`x`, x0.toString()).replace(`y`, y0.toString())
		z = evaluatex(zString1, {}, {latex:true})();
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
			on:input={roundCos} 
			on:input={show} 
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
			on:input={roundCos}
			on:input={show} 
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
<div class="bg-gray-800 p-4 rounded-lg my-3 mx-5">
		<Katex>z=f(x,y)={zString}</Katex><br>
		<Katex>x_0={x0}</Katex>,
		<Katex>y_0={y0}</Katex>,
		<Katex>dx={dx}</Katex>,
		<Katex>dy={dy}</Katex><br><br>
		Stąd mamy:<br>

		<Katex>{KatexString}=f({x},{y})=f({x0}+{dx},{x0}+{dy})</Katex><br><br>
		Teraz korzystamy ze wzoru:<br>
		<Katex>f(x_0+dx,y_0+dy) \approx f(x_0,y_0)+dz</Katex><br><br>
		Żeby obliczyć: <br>

		<Katex>f(x_0,y_0)=f({x0},{y0})={zString1}={z}</Katex><br><br>

<!--W tym miejscu trzeba policzyć dwie pochodne i potem podstawić pod wzory-->
		Wyznaczamy wartość pochodnych cząstkowych w punkcie <Katex>(x_0,y_0)</Katex> <br>
		<Katex>f'_x(x,y)=</Katex><br><br>

		Obliczamy różniczkę zupełną:<br>
		<Katex>dz=f'_x(x_0,y_0)dx+f'_y(x_0,y_0)dy=</Katex>


</div>
