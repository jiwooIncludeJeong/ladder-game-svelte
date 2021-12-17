<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	let num = 1;
	let select = 1;

</script>

<main>
	<h1>벙커키즈 뽑기</h1>
	<div class="enter">
		<p>몇 명 참여합니까?</p>
		<input type="number" bind:value={num} placeholder="몇 명 참여합니까?" min={1}  >
	</div>
	<div class="enter">
		<p>몇 명 당첨입니까?</p>
		<input type="number" bind:value={select} placeholder="몇 명의 당첨입니까?" min={1}  max={num}>
	</div>
	<div class="buttonArea">
		<a href="/play?num={num}&select={select}">
			<button>
				확인
			</button>
		</a>
	</div>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }
    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    input {
        width: 80px;
        align-self: center;
    }

    button {
				padding:12px;
        width:200px;
        background-color: #ff3e00;
        color:white;
        border: 1px solid white;
        align-self: center;
    }

    .enter {
        display: flex;
        flex-direction: column;
    }
    .buttonArea {
        margin-top: 100px;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
		@media only screen and (max-width: 640px){
        h1 {
            font-size:1.8em;
        }
		}
</style>
