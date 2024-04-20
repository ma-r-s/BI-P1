<script>
	import { Button } from '$lib/components/ui/button';
	import { Textarea } from '$lib/components/ui/textarea';

	let reviewText = '';
	let reviewResult = '?';
	async function enviarReseña() {
		const encodedReview = encodeURIComponent(reviewText);
		const response = await fetch(
			`https://fastapi-xw6s.onrender.com/predict/?review=${encodedReview}`
		);
		const data = await response.json();
		console.log(data);
		reviewResult = data.predicted_score;
	}
</script>

<div class="flex h-dvh flex-col justify-center">
	<div class="mx-auto w-full max-w-[600px]">
		<div class="mb-10 text-xl font-bold">Calificador de reseñas</div>
		<div class="mb-10 font-bold">Result: {reviewResult}</div>
		<Textarea class="mb-6" placeholder="Ingresa la reseña aquí" bind:value={reviewText} />
		<Button on:click={enviarReseña}>Enviar</Button>
	</div>
</div>
