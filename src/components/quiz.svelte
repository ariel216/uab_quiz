<script>
    import questions from './data.json';

    //const questions = [{"id":1, "question":"Pregunta 1"},{"id":2, "question":"Pregunta 2"},{"id":3, "question":"Pregunta 3"}];
	let id = 0;
    let question = "";

    function random() {
        let valor = Math.floor((Math.random() * (questions.length - 1 + 1)) + 1);
        if(valor===id){
            random()
        }else{
            id = valor;
        }         
    }
    function getById(id){
        question = questions.find(obj => obj.id === Number(id));
    }

	function handleAleatory() {
        random();
        getById(id);
	}
</script>

<section class="flex flex-col items-center justify-center mt-14">    
    <div class="grid grid-flow-row grid-cols-3 gap-2 items-center justify-items-center">
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800" on:click={handleAleatory}>Aleatorio</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Verdadero Falso</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Abiertas</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Completar</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Multiopciones</button>
    </div>
    {#if id>0}
        <article class="aspect-video bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-sm text-center mt-5">
            <h2 class="text-2xl">Pregunta {id}</h2>
            <p class="text-balance mt-3">{question.question}</p>
            <div class="inline-flex gap-3 mt-3">
                <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300">Verdadero</button>
                <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300">Falso</button>
            </div>            
        </article>     
    {:else}
        <article class="aspect-video bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-md text-center mt-5">
            <h2 class="text-2xl">Elige el tipo de pregunta</h2>          
        </article>    
    {/if}
         
</section>