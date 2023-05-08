<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";
  let createdContact;
  let createdContacts = [];

  function addContact() {
    if (
      name.trim().length == 0 ||
      title.trim().length == 0 ||
      image.trim().length == 0 ||
      description.trim().length == 0
    ) {
      formState = "invalid";
      return;
    }
    createdContact = {
      name: name,
      jobTitle: title,
      imageUrl: image,
      desc: description,
    };
    createdContacts = [
      ...createdContacts,
      {
        id: Math.random(),
        name: name,
        jobTitle: title,
        imageUrl: image,
        desc: description,
      },
    ];
    formState = "done";
  }

  function deleteFirst() {
    createdContacts = createdContacts.slice(1)
  }
  function deleteLast() {
    createdContacts = createdContacts.slice(0, -1)
  }
</script>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<!-- <button on:click|once={addContact}>Add Contact Card</button>
<button on:click|capture={addContact}>Add Contact Card</button>
<button on:click|stopPropagation={addContact}>Add Contact Card</button>
<button on:click|preventDefault={addContact}>Add Contact Card</button> -->
<button on:click={addContact}>Add Contact Card</button>
<button on:click={deleteFirst}>Delete First</button>
<button on:click={deleteLast}>Delete Last</button>

{#if formState === "done"}
  <ContactCard
    userName={name}
    jobTitle={title}
    {description}
    userImage={image}
  />

  <ContactCard
    userName={createdContact.name}
    jobTitle={createdContact.jobTitle}
    description={createdContact.desc}
    userImage={createdContact.imageUrl}
  />
  <!-- {/if}
{#if formState === 'invalid'} -->
{:else if formState === "invalid"}
  <p>Invalid Input</p>
{:else}
  <p>please enter some data and hit the button</p>
{/if}



{#if formState === "invalid"}
  <p>Invalid Input</p>
{:else}
  <p>please enter some data and hit the button</p>
{/if}

{#each createdContacts as contact, index (contact.id)}
<h2># {index + 1}</h2>
  <ContactCard
    userName={contact.name}
    jobTitle={contact.jobTitle}
    description={contact.desc}
    userImage={contact.imageUrl}
  />
  {:else}
  <p>Please start adding some contacts, we found none!</p>
{/each}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
