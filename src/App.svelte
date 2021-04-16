<script>
	let w = window
	let topX = 0
	let topY = 0
	let scale = 1
	let minArmSize = 100
	let maxArmSize = 200
	const colors = ['#CBE4F9', '#CDF5F6', '#EFF9DA', '#F9EBDF', '#F9D8D6', '#D6CDEA']
	const r = (min, max)  => { // min and max included 
  			return Math.floor(Math.random() * (max - min + 1) + min)
		}
	let color = colors[r(0, 5)]
	
	const createTriangle = (context) => {
		
		const firstLine = (context, x1, y1, x2, y2) => {
			context.beginPath()
			context.moveTo(x1, y1)
			context.lineTo(x2, y2)
		}

		const second = (context, x, y) => (
			context.lineTo(x, y)
		)

		const third = () => {
			context.closePath()
		}


		let x2 = r(topX, topX + r(minArmSize, maxArmSize))
		let y2 = r(topY, topY + r(minArmSize, maxArmSize))
		firstLine(context, topX, topY, x2, y2)
		if(y2 > topY){
		
			topY = y2
		}

		if(x2 > topX) {
			topX = x2
		}
	x2 = r(topX, (r(minArmSize, maxArmSize) + topX) * r(1.5, 2))
	y2 = r(topY, r(minArmSize, maxArmSize * r(1, 1.5)) + topY)
	var grd = context.createRadialGradient(0, 0, 1000, 1680, 800, 1000);
	
		grd.addColorStop(0, colors[r(0, 5)]);
		grd.addColorStop(1, colors[r(0, 5)]);
		second(context, x2, y2)
		if(y2 > topY){
		
		topY = y2
	}

	if(x2 > topX) {
		topX = x2
	}
	third()
	context.lineWidth = 10;


	context.fillStyle = grd;
	context.fill();
		
	}
	const increment = () => {
		color = colors[r(0, 5)]
		var canvasElement = document.querySelector("#myCanvas");
		var context = canvasElement.getContext("2d");
		if(topX > 1680 || topY > 800){
			context.clearRect(0, 0, canvasElement.width, canvasElement.height)
			topX = 0
			topY = 0
		}
	
		createTriangle(context)
	}
</script>

<main on:click="{increment}">
	<div class="content">
		<h1 style="{`color: ${color};`}">Daniel Szerszeń</h1>
		<h2>FullStack developer</h2>
	</div>
	<canvas id="myCanvas" width="{w.innerWidth}" height="{w.innerHeight}"></canvas>
</main>

<style>
	.content{
		position: absolute;
		z-index:2;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%)
	}
	canvas{
		position: absolute;
		left:0;
		top: 0;
	}
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h2 {
		color: gray;
		text-transform: uppercase;
		font-size: 1.5em;
		font-weight: 100;
	}
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 6em;
		font-weight: 200;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>