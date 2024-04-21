<script>
	import { Button } from '$lib/components/ui/button';
	import { Textarea } from '$lib/components/ui/textarea';
	import { Input } from '$lib/components/ui/input/index.js';
	let reviewText = '';
	let retrainedText = '';
	let reviewResult;
	let retrainedResult;
	let file;
	async function enviarReseña() {
		const encodedReview = encodeURIComponent(reviewText);
		const response = await fetch(
			`https://fastapi-xw6s.onrender.com/predict/?review=${encodedReview}`
		);
		const data = await response.json();
		console.log(data);
		reviewResult = data.predicted_score;
	}

	async function enviarReseña2() {
		const encodedReview = encodeURIComponent(retrainedText);
		const response = await fetch(
			`https://fastapi-xw6s.onrender.com/predict/?review=${encodedReview}`
		);
		const data = await response.json();
		console.log(data);
		retrainedResult = data.predicted_score;
	}

	// Función para cargar y reentrenar el sistema con nuevos datos
	async function reentrenarSistema() {
		// Aquí iría el código para cargar y reentrenar el sistema
		// Ejemplo: fetch('/reentrenar-sistema', { method: 'POST', body: formData });
		// Después de reentrenar, se podría volver a probar el sistema
	}
</script>

<div class="my-12 flex-col text-pretty">
	<div class="mx-auto w-full max-w-[800px]">
		<!-- Título del proyecto -->
		<div class="mb-10 text-3xl font-bold">Proyecto de Análisis de Reseñas Turísticas</div>

		<!-- Explicación del proyecto -->
		<div class="mb-10 mt-8">
			<p class="mb-4">
				Este proyecto de análisis de datos turísticos en los Alpes se realiza debido a la necesidad
				de analizar las características de sitios turísticos que los hacen atractivos para turistas
				locales o de otros países, ya sea para ir a conocerlos o recomendarlos. Este sistema es
				requerido por Ministerio de Comercio, Industria y Turismo de Colombia, la Asociación
				Hotelera y Turística de Colombia – COTELCO, y reconocidas cadenas hoteleras como Hilton,
				Hoteles Estelar y Holiday Inn, así como hoteles más pequeños en diferentes municipios del
				país.
			</p>
			<p class="mb-4">
				El objetivo principal del proyecto fue analizar las características de los sitios turísticos
				en los Alpes que hacen que sean atractivos para turistas. Para ello, se emplearon técnicas
				de análisis de datos, incluyendo un modelo de regresión logística, así como técnicas de
				procesamiento de lenguaje natural como stemming y matrices TF-IDF.
			</p>
			<p class="mb-4">
				Este sistema desarrollado permite predecir la calificación de una reseña turística a partir
				del texto de la misma. Estas predicciones son fundamentales para los actores del turismo, ya
				que les brindan información valiosa para tomar decisiones estratégicas con el fin de mejorar
				la popularidad de los sitios turísticos en los Alpes y fomentar el turismo en la región.
			</p>
		</div>

		<!-- Sección para probar el sistema -->
		<div class="mb-10 text-xl font-bold">API de Prediccion de Score</div>
		<Textarea class="mb-6" placeholder="Ingresa la reseña aquí" bind:value={reviewText} />
		<div class=" mb-10 flex justify-between font-bold">
			<Button on:click={enviarReseña}>Enviar</Button>
			{#if reviewResult}
				<div class="">Resultado de la Predicción: {reviewResult}</div>
			{/if}
		</div>

		<!-- Sección para cargar datos de entrenamiento y reentrenar el sistema -->
		<div class="mb-10 text-2xl font-bold">Reentrenamiento del Modelo</div>
		<p class="mb-6">
			En esta sección, puedes subir tus propios datos de entrenamiento para reentrenar el sistema de
			análisis de reseñas turísticas. Esto permite adaptar el modelo a nuevas tendencias o
			preferencias de los turistas. Después de reentrenar el sistema, podrás probar el nuevo modelo
			con reseñas adicionales para evaluar su rendimiento.
		</p>
		<div class="mb-6 flex justify-between">
			<Input class="max-w-80" type="file" bind:file />
			<Button on:click={enviarReseña}>Reentrenar</Button>
		</div>

		<div class="mb-24">
			<p class="mb-4">
				Reentrenar el sistema con nuevos datos de entrenamiento puede abrir la puerta a una variedad
				de nuevos usos no relacionados al problema inicial. Por ejemplo:
			</p>
			<ul class="ml-8 list-disc">
				<li class="mb-2">
					Análisis de Sentimiento en Otros Sectores: El modelo entrenado con reseñas turísticas
					podría aplicarse para analizar el sentimiento de los clientes en otras industrias, como
					restaurantes, productos electrónicos, o servicios de salud.
				</li>
				<li class="mb-2">
					Detección de Fraude: Utilizando técnicas similares de procesamiento de lenguaje natural,
					el modelo podría identificar patrones de fraude en transacciones financieras o en redes
					sociales.
				</li>
				<li class="mb-2">
					Clasificación Automática de Documentos: El modelo podría ser adaptado para clasificar
					automáticamente documentos legales, médicos o académicos en función de su contenido y
					tono.
				</li>
				<li>
					Personalización de Contenidos: Basándose en las preferencias y opiniones de los usuarios,
					el modelo podría recomendar contenido personalizado en plataformas de streaming, redes
					sociales, o sitios de comercio electrónico.
				</li>
			</ul>
			<div class="my-10 text-xl font-bold">API de Prediccion de Score Reentrenado</div>
			<Textarea
				class="mb-6"
				placeholder="Ingresa el texto a predecir aquí"
				bind:value={retrainedText}
			/>
			<div class="flex justify-between font-bold">
				<Button on:click={enviarReseña2}>Enviar</Button>
				{#if retrainedResult}
					<div class="">Resultado de la Predicción: {retrainedResult}</div>
				{/if}
			</div>
		</div>
		<div class="mb-10">Inteligencia de Negocios - 2024</div>
		<div class="mb-32 flex justify-around">
			<p>Santiago Ramírez</p>
			<p>Mario Ruíz</p>
			<p>Santiago Gelvez</p>
		</div>
	</div>
</div>
