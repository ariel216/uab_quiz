<script>
import data from './banco1.json';

    const total = data.questions.length;
    const questions = data.questions;
    let count = 1;
	let question = "";
    let withAnswer = false;
    let myAnswers = []; //
    let nextBtn = true;
    let state = false; //
    let results = false; //
    
    const handleInit = ()=>{        
        myAnswers = [];
        setQuestion();
        state=true;
        results=false;
        count=1;
        nextBtn=true;
    }

    const setQuestion = ()=>{
        if(count > 0 && count<=total){           
            question = questions.find(obj => obj.id === Number(count));
        }        
    }
        
    const handleNext = ()=>{     
        withAnswer = false;
        count++;
        setQuestion(); 
        var ele = document.getElementsByName("answer");
        for(let i=0;i<ele.length;i++)
            ele[i].checked = false;
    }

    const handleAnswer =(e)=>{ 
        withAnswer = true; 
        if(count==total){
            //question:"" 
            nextBtn= false; 
        }  
        myAnswers.push({
            id_question: question.id,
            id_answer: Number(e.target.value),
            correct_answer: question.answer,
            answer: question.answers.find(obj => obj.id === Number(question.answer)),
            question:question.question
        });
        //console.log(myAnswers);
    }

    const showResults =()=>{
        results=true;
        //console.log('muestra resultados');
    }

</script>

<section class="flex flex-col items-center justify-center mt-14 ">  
    {count} | {total}
    {#if !state}  
        <div class="gap-2 items-center justify-items-center">        
            <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300" on:click={handleInit}>Iniciar</button>
        </div>    
    {:else}
        {#if !results}  
            <article class="block h-2/3 w-1/2 bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-sm text-center mt-5">
                <h2 class="text-2xl">Pregunta {question.id}</h2>
                <p class="text-balance mt-3">{question.question}</p>
                <div class="inline-flex gap-3 mt-8">
                    {#each question.answers as { id, label }, i}
                        <label for={id} class="hover:cursor-pointer">{label}</label>
                        <input type="radio" name="answer" id={id} value={id} class="w-6" on:change={handleAnswer}>
                    {/each}                
                </div>            
            </article>     
            <div class="flex mt-8">
                {#if withAnswer}
                    {#if nextBtn}
                        <button class="bg-cyan-700 max-w-fit px-3 py-2 rounded-md hover:bg-cyan-800" on:click={handleNext}>Siguiente</button>
                    {:else}
                        <button class="bg-cyan-700 max-w-fit px-3 py-2 rounded-md hover:bg-cyan-800" on:click={showResults}>FINALIZAR</button>
                    {/if}                    
                {/if}            
            </div>
        {:else}            
            <article class="flex-1 h-2/3 w-1/2 bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-md mt-5">
                <h3 class="text-2xl text-center">Resultados</h3>                
                {#each myAnswers as { id_question, question, answer, id_answer, correct_answer }, i}
                    <div class="flex flex-col ml-4 mt-4 space-y-2">
                        <p>{id_question} - <span class="text-sm">{question}</span></p>
                        {#if id_answer!==correct_answer}
                            <p class="bg-red-500 w-fit px-2 rounded-md">{answer.label}</p>
                        {:else}
                            <p class="bg-green-500 w-fit px-2 rounded-md">{answer.label}</p>
                        {/if}
                        
                    </div>
                {/each}
                <div class="mt-5 text-center">
                    <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300" on:click={handleInit}>Reiniciar</button>       
                </div>                
            </article> 
        {/if}
    {/if}     
</section>