<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../UI/Button.svelte";
  import TextInput from "../UI/TextInput.svelte";
  import Modal from "../UI/Modal.svelte";

  let title = "";
  let subtitle = "";
  let address = "";
  let email = "";
  let description = "";
  let imageUrl = "";
  const dispatch = createEventDispatcher();

  function submitForm() {
    console.log("Submit")
    dispatch("save", {
      title: title,
      subtitle: subtitle,
      address: address,
      email: email,
      description: description,
      imageUrl: imageUrl,
    });
  }

  function cancel() {
    dispatch('cancel')
  }
</script>

<style>
     form {
    /* width: 30rem;
    max-width: 90%;
    margin: auto; */
    width: 100%
  }
</style>

<!-- <form on:submit|preventDefault={submitForm}>
  <TextInput
    id="title"
    label="Title"
    type="text"
    value={title}
    on:input={(event) => (title = event.target.value)}
  />
  <TextInput
    id="subtitle"
    label="Subtitle"
    type="text"
    value={subtitle}
    on:input={(event) => (subtitle = event.target.value)}
  />
  <TextInput
    id="address"
    label="Address"
    type="text"
    value={address}
    on:input={(event) => (address = event.target.value)}
  />
  <TextInput
    id="imageUrl"
    label="image URL"
    type="text"
    value={imageUrl}
    on:input={(event) => (imageUrl = event.target.value)}
  />
  <TextInput
    id="email"
    label="E-Mail"
    type="email"
    value={email}
    on:input={(event) => (email = event.target.value)}
  />
  <TextInput
    id="description"
    label="Description"
    controlType="textarea"
    value={description}
    on:input={(event) => (description = event.target.value)}
  /> -->
  <!-- <Button type="submit" caption="Save" /> -->
  <!-- <Button type="submit">Save</Button>
</form> -->

<Modal on:cancel>
    <form on:submit|preventDefault={submitForm}>
        <TextInput
          id="title"
          label="Title"
          type="text"
          value={title}
          on:input={(event) => (title = event.target.value)}
        />
        <TextInput
          id="subtitle"
          label="Subtitle"
          type="text"
          value={subtitle}
          on:input={(event) => (subtitle = event.target.value)}
        />
        <TextInput
          id="address"
          label="Address"
          type="text"
          value={address}
          on:input={(event) => (address = event.target.value)}
        />
        <TextInput
          id="imageUrl"
          label="image URL"
          type="text"
          value={imageUrl}
          on:input={(event) => (imageUrl = event.target.value)}
        />
        <TextInput
          id="email"
          label="E-Mail"
          type="email"
          value={email}
          on:input={(event) => (email = event.target.value)}
        />
        <TextInput
          id="description"
          label="Description"
          controlType="textarea"
          value={description}
          on:input={(event) => (description = event.target.value)}
        />
        <!-- <Button type="submit" caption="Save" /> -->
        <!-- <Button type="submit">Save</Button> -->
      </form>
      <div>
        <Button type="button" mode="out;one" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm}>Save</Button>
      </div>
</Modal>