<script>
  import { onMount } from 'svelte';

  let files = [];

	function validate(event) {
		console.log(event.type)
		debugger;
	}
  function handleFileInput(event) {
		console.log(event.type)
    const fileList = event.target.files;
    for (let i = 0; i < fileList.length; i++) {
      const file = fileList[i];
      files = [...files, file];
    }
		debugger;
		event.target.value = '';
  }

  function removeFile(index) {
    files = files.filter((_, i) => i !== index);
  }
	
  onMount(() => {
    // Clear the file input on mount to prevent retaining previous selections
    const fileInput = document.getElementById('file-input');
    fileInput.value = '';
  });
</script>

<style>
  .file-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
  }

  .file-name {
    margin-right: 8px;
  }

  .file-actions {
    display: flex;
    align-items: center;
  }

  .file-actions button {
    margin-left: 8px;
  }
</style>

<h2>File Input Form</h2>

<form on:submit|preventDefault={validate}>
	{#if files.length > 0}
	  <h3>Attached Files</h3>
	  {#each files as file, index}
	    <div class="file-item">
				<input type="file" name={`a[0].b[${index}]`} bind:value={file}>
	      <span class="file-name">{file.name}</span>
	      <div class="file-actions">
	        <button on:click={() => removeFile(index)}>Remove</button>
	      </div>
	    </div>
	  {/each}
	{/if}
	{files.length}
	<input type="file" id="file-input" multiple on:change={handleFileInput}>
	<input type="submit" value="Send Request" />
</form>
