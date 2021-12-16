<script context="module">
	import { browser, dev } from '$app/env';

	// we don't need any JS on this page, though we'll load
	// it in dev so that we get hot module replacement...
	export const hydrate = dev;

	// ...but if the client-side router is already loaded
	// (i.e. we came here from elsewhere in the app), use it
	export const router = browser;

	// since there's no dynamic data here, we can prerender
	// it so that it gets served as a static asset in prod
	export const prerender = true;
</script>

<script lang="ts">
	import {page} from '$app/stores';
	const num = $page.query.get('num');
	const select = $page.query.get('select');
	let name = [];
	let arr = [];
	let showModal = false;
	let timer = 3;
	let timerRef ;
	let selector =[];

	for(let i =0 ; i < num; i++){
		arr.push(i);
	}

	const inputName = (value:string, index:number) => {
		name[index] = value;
	}
	const onClickButton = () => {
		if(name.length === 0 || name.includes('')){
			return;
		}else {

		while(selector.length < select){
			const selected = name[Math.floor(Math.random()*(num))];
			if(selector.includes(selected)){
				continue;
			} else {
				selector.push(selected)
			}
		}
		showModal= true;
		timerRef = setInterval(()=>{
			if(timer > 0){
			timer--;
			}
			else {
				clearInterval(timerRef)
			}
		},1000)
		}
	}
	 $ : if(timer === 0 && !showModal){
		timer = 3;
		clearInterval(timerRef);
		selector=[];
	}
</script>

<main>
	<h1>두구두구</h1>
	<div class='names'>
		{#each arr as n, index (index)}
			<div class='nameWrapper'>
				<p class='name'>이름 :</p>
				<input on:change={(e) => {inputName(e.target.value, index)}} class="nameInput" type='text'/>
			</div>
			{/each}
	</div>
	<button on:click={onClickButton}>
		시작해보자
	</button>
		{#if showModal === true}
			<div class={'outerModal'} on:click={()=>{showModal=false}}>
				<div class='innerModal'>
					{#if timer === 0 }
						{#each selector as s}
						<h1>{s}</h1>
							{/each}
						{:else}
					<h1>{timer}</h1>
						{/if}
				</div>
			</div>
			{/if}
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
				position: relative;
    }
    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }
		div .nameWrapper{
						display: flex;
						flex-direction: row;
				align-items: center;
		}
    button {
        padding:12px;
        width:200px;
        background-color: #ff3e00;
        color:white;
        border: 1px solid white;
				align-self: center;
    }
		 .nameInput {
		}
		.names {
				display: flex;
				flex-direction: column;
		}

		.name {
				font-size: 24px;
				margin-right: 12px;
		}
		.outerModal {
				width:100vw;
				height:100vh;
				display: flex;
				flex-direction: column;
				align-self: center;
				justify-content: center;
				background-color: rgba(0,0,0,0.4);
				position: absolute;
				top:0;
		}
    .innerModal {
        width:200px;
        padding:12px;
        display: flex;
        flex-direction: column;
        align-self: center;
        justify-content: center;
        background-color: white;
				border-radius: 12px;
    }


    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
