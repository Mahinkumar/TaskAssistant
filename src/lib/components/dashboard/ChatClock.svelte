<script lang="ts">
    import { BookOpenText, BookText, Bot, SendHorizontal } from 'lucide-svelte';
	import PomodoroClock from './PomodoroClock.svelte';
    import Typewriter, { cascade, concurrent, scramble } from 'svelte-typewriter'
	import { fade } from 'svelte/transition';
	import { enhance } from '$app/forms';
	import { type PageData, type ActionData } from '../../../routes/[[app]]/$types';

    let { forms }: { forms: ActionData } = $props();

    let clockmode = $state("Ai-Brief") 
    let ai_text = $state(forms?.chatCompletion.choices[0].message.content||"Hello! I'm here to help you. Just let me know how I can assist you today.")

    

</script>
<div class="h-96 w-full flex flex-col items-center">
    <div class="w-48 h-8 border-2 border-gray-500 flex rounded-b-lg justify-center items-center">
        <button aria-label="Work Mode" class="transition-all duratiion-700 h-8 w-10 hover:text-gray-800  flex items-center justify-center {clockmode == 'Work' ? 'text-black' : 'text-gray-400'}" onclick={()=>clockmode='Work'}><BookOpenText/></button>
        <button aria-label="Ai-Brief Mode" class="transition-all duratiion-700 h-8 w-10 hover:text-gray-800 flex items-center justify-center {clockmode == 'Ai-Brief' ? 'text-black' : 'text-gray-400'}" onclick={()=>clockmode='Ai-Brief'}><Bot /></button>
        <button aria-label="Switch Work/Rest Modes" class="transition-all duratiion-700 h-8 w-20 text-lg font-semibold" onclick={()=> clockmode = (clockmode == 'Ai-Brief' ? 'Work' : 'Ai-Brief')}>{clockmode}</button>
    </div>
    <form class="w-full flex items-star justify-evenly h-full relative" method="post" use:enhance>
        {#if clockmode=="Ai-Brief"}
        <Typewriter>
            <div use:cascade={{ unwriteInterval: 100 }} class="font-semibold text-4xl p-8 w-[64rem] ml-[5%] text-left">
                {ai_text}
            </div>
        </Typewriter>
        <div class="absolute bottom-10 rounded-md w-[90%] flex justify-center items-center border-2">  
            <button class="w-[10%] flex items-center justify-center" formaction="?/get_ai"><SendHorizontal /></button> 
            <input type="text" name="prompt" class="w-[90%] h-full border-2"/>
        </div>
        
        {:else}
        <div class="h-full flex w-full items-center justify-evenly" in:fade>
            <PomodoroClock/>
            <div class="w-[50%] text-2xl h-full flex flex-col justify-center items-start space-y-16">
                <div class="font-semibold text-4xl">Start the Timer whenever you are ready.</div>
                <div>
                    <div class="flex"><h1 class="font-bold">Current Task: &nbsp; </h1> Linux Kernel Development</div>
                    <div class="flex"><h1 class="font-bold">Next Task: &nbsp; </h1> Break - 5 Minutes</div>
                </div>
            </div>
        </div>
        {/if}
        
    </form>
</div>