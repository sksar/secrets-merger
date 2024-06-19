<script>
	import {onMount} from "svelte";

    let SECRETS = [];
    function addInput() {
        SECRETS.push({ key: '', value: '' });
        SECRETS = SECRETS;
	}

    onMount(() => {
		addInput();
	});

    // Outputs
	let mergedSecrets = '';
    let mergedKeys = '';
	function merge() {
		mergedSecrets = '';
		mergedKeys = '';
		for (let i = 0; i < SECRETS.length; i++) {
            if (i === 0) {
                mergedSecrets += SECRETS[i].value
				mergedKeys += SECRETS[i].key
			}
            else {
                mergedSecrets += `|${SECRETS[i].value}`
				mergedKeys += `|${SECRETS[i].key}`
			}
        }
	}
</script>

<h1>Secrets Merger</h1>
<p>Merge your secrets into one variable</p>

<h2>Secrets</h2>

{#each SECRETS as secret, i}
	<div style="margin-bottom: 5px;">
		<input type="text" bind:value={secret.key} placeholder="Name" on:input={merge}/>
		<input type="text" bind:value={secret.value} placeholder="Value" on:input={merge}/>
	</div>
{/each}

<button on:click={addInput}>Add secret</button>


<h2>Result</h2>
<pre><code>{mergedKeys}</code></pre>
<pre><code>{mergedSecrets}</code></pre>
<pre><code>{btoa(mergedSecrets)}</code></pre>
