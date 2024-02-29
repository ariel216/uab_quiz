<script>
import data from './banco1.json';

    const total = data.questions.length;
    const questions = data.questions;
    let count = 0;
	let question = "";
    let withAnswer = false;
    let myAnswers = [];
    let labelBtnNext;
    let finalizado = false;
    const setQuestion = (id_param)=>{
        if(id_param > 0 && id_param<=total){           
            question = questions.find(obj => obj.id === Number(id_param));
            count++;
        }        
    }
    const handleInit = ()=>{    
        count=1
        myAnswers = [];    
        setQuestion(count);
    }
        
    const handleNext = ()=>{     
        withAnswer = false;   
        setQuestion(count); 
        var ele = document.getElementsByName("answer");
        for(var i=0;i<ele.length;i++)
            ele[i].checked = false;
    }

    const handleAnswer =(e)=>{           
        //verifica conteo
        if(count<=total){
            labelBtnNext= 'Siguiente';
            myAnswers.push({
                id_question: question.id,
                id_answer: Number(e.target.value),
                correct_answer: question.answer
            });
            console.log(myAnswers);
        }else{
            labelBtnNext= 'FINALIZAR';
            //mostrar resultados            
        }    
        if(count==(total+2)){
            finalizado=true;
        }
        withAnswer = true;   
    }

</script>

<section class="flex flex-col items-center justify-center mt-14 ">    
    <div class="gap-2 items-center justify-items-center">
        {#if count==0}
            <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300" on:click={handleInit}>Iniciar</button>       
        {/if}
    </div>
    {#if count>0}        
        {#if !finalizado}
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
                    <button class="bg-cyan-700 max-w-fit px-3 py-2 rounded-md hover:bg-cyan-800" on:click={handleNext}>{labelBtnNext}</button>
                {/if}            
            </div>
        {:else}            
            <article class="flex-1 h-2/3 w-1/2 bg-white bg-opacity-15 shadow-lg rounded-2xl p-4 w-md text-center mt-5">
                <h3 class="text-2xl">Resultados</h3>
                <div class="grid grid-cols-10 space-y-2">
                    {#each myAnswers as { id_question, id_answer, correct_answer }, i}
                        {#if id_answer===correct_answer}
                            <span class="bg-emerald-600 w-10 p-2 rounded-full align-middle">
                                <p title={correct_answer}>{id_question}</p>
                            </span>
                        {:else}
                            <span class="bg-red-500 w-10 p-2 rounded-full align-middle">
                                <p title={correct_answer}>{id_question}</p>
                            </span>
                        {/if}                        
                    {/each}
                </div>
                <button class="text-slate-900 bg-slate-50 max-w-fit px-2 py-1 rounded-md hover:bg-slate-300" on:click={handleInit}>Reiniciar</button>       
            </article> 
        {/if}
    {/if}
         
</section>