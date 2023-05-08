<script>
  let enteredPassword = "";
  let passwordValidity = "short";
  let passwordList = [];

  $: if (enteredPassword.trim().length < 5) {
    passwordValidity = "short";
  } else if (enteredPassword.trim().length > 10) {
    passwordValidity = "long";
  } else {
    passwordValidity = "valid";
  }

  function addPassword() {
    passwordList = [...passwordList, enteredPassword];
  }

  function addPasswordwithCheck() {
    if (passwordValidity === "valid") {
      passwordList = [...passwordList, enteredPassword];
    }
  }

  function removePassword(index) {
    passwordList = passwordList.filter((pw, i) => i !== index);
  }
</script>

<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
  <li>Add a password input field and save the user input in a variable.</li>
  <li>
    Output "Too short" if the password is shorter than 5 characters and "Too
    long" if it's longer than 10.
  </li>
  <li>
    Output the password in a paragraph tag if it's between these boundaries.
  </li>
  <li>Add a button and let the user add the passwords to an array.</li>
  <li>Output the array values (= passwords) in a unordered list (ul tag).</li>
  <li>Bonus: If a password is clicked, remove it from the list.</li>
</ol>

<input type="password" bind:value={enteredPassword} />
<button on:click={addPasswordwithCheck}>Add Password to list</button>
{#if enteredPassword.trim().length < 5}
  <p class="error">Too short!</p>
{:else if enteredPassword.trim().length > 10}
  <p class="error">Too long!</p>
{:else}
  <p>{enteredPassword}</p>
  <button on:click={addPassword}>Add Password to list</button>
{/if}

{#if passwordValidity === "short"}
  <p class="error">Too short!</p>
{:else if passwordValidity === "long"}
  <p class="error">Too long!</p>
{:else}
  <p>Password: {enteredPassword}</p>
{/if}

<ul>
  {#each passwordList as password, index (password)}
    <li on:click={removePassword.bind(this, index)}>#{index + 1} {password}</li>
  {/each}
</ul>

<style>
  .error {
    color: red;
  }
</style>
