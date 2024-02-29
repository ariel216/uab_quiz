<script>
    import data from './banco1.json';

    const total = data.questions.length;
    const questions = data.questions;
    let id = 0;
	let question = "";
    //console.log(total);
    
    const setQuestion = (id_param)=>{
        if(id_param > 0 && id_param<=total){           
            question = questions.find(obj => obj.id === Number(id_param));
            id++;
        }        
    }
    function handleInit (){        
        setQuestion(1);
    }
    handleInit();
    
    function handleNext (){        
        setQuestion(id);        
    }

</script>

<section class="flex flex-col items-center justify-center mt-14">    
    <div class="grid grid-flow-row grid-cols-3 gap-2 items-center justify-items-center">
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800" on:click={handleInit}>Todos</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Verdadero Falso</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Abiertas</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Completar</button>
        <button class="bg-cyan-700 max-w-fit px-2 py-1 rounded-md hover:bg-cyan-800">Multiopciones</button>
    </div>
    {#if id>0}
        <article class="block h-2/3 w-1/2 bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-sm text-center mt-5">
            <h2 class="text-2xl">Pregunta {id}</h2>
            <p class="text-balance mt-3">{question.question}</p>
            <div class="inline-flex gap-3 mt-3">
                <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300">Verdadero</button>
                <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300">Falso</button>
            </div>            
        </article>     
        <div class="flex mt-4">
            <button class="text-slate-900 bg-teal-200 max-w-fit px-4 py-2 rounded-md hover:bg-teal-300" on:click={handleNext}>Siguiente</button>
        </div>
    {:else}
        <article class="aspect-video bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-md text-center mt-5">
            <h2 class="text-2xl">Elige el tipo de pregunta</h2>          
        </article>    
    {/if}
         
</section>