<script>
  import ContactCard from "./ContactCard.svelte";

  export let name;
  export let age;
  let otherName = "Harsha";
  let otherAge = 30;

  let title = "";
  let description = "";
  let image = "";

  $: upperCaseName = otherName.toUpperCase();

  $: console.log(otherName);

  $: if (otherName === "Deepika") {
    otherAge = 25;
  }

  //   function incrementAge() {
  //     otherAge += 1;
  //   }

  const incrementAge = () => {
    otherAge += 1;
  };

  function changeName() {
    otherName = "Deepika";
  }

  function nameInput(event) {
    // otherName = event.target.value
    const enteredValue = event.target.value;
    otherName = enteredValue;
  }
</script>

<h1>Hello {name.toUpperCase()}, my age is {age}!</h1>
<h1>Hello {otherName}, my age is {otherAge}!</h1>
<h1>Hello {upperCaseName}, my age is {otherAge}!</h1>
<button on:click={incrementAge}>Change my Age</button>
<!-- <button on:click={changeName}>Change my Name</button> -->
<!-- <input type="text" value={otherName} on:input={nameInput} /> -->
<input type="text" bind:value={otherName} />
<input type="text" bind:value={title} />
<input type="text" bind:value={image} />
<textarea bind:value="{description}" />
<ContactCard userName={otherName} jobTitle={title} {description} userImage="{image}" />

<style>
  h1 {
    color: purple;
  }
</style>
