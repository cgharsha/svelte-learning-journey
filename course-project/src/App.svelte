<script>
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import MeetupItem from "./Meetups/MeetupItem.svelte";
  import Button from "./UI/Button.svelte";
  import Header from "./UI/Header.svelte";
  import TextInput from "./UI/TextInput.svelte";
  let title = '';
  let subtitle = '';
  let address = '';
  let email = '';
  let description = '';
  let imageUrl = '';

  let meetups = [
    {
      id: "m1",
      title: "Coding Bootcamp",
      subtitle: "Learn to code in 2 hours",
      description:
        "In this meetup, we will have some experts that teach you how to code!",
      imageUrl:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Caffe_Nero_coffee_bar%2C_High_St%2C_Sutton%2C_Surrey%2C_Greater_London.JPG/800px-Caffe_Nero_coffee_bar%2C_High_St%2C_Sutton%2C_Surrey%2C_Greater_London.JPG",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "code@test.com",
    },
    {
      id: "m2",
      title: "Swim Together",
      subtitle: "Let's go for some swimming",
      description: "We will simply swim some rounds!",
      imageUrl:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/6/69/Olympic_swimming_pool_%28Tbilisi%29.jpg/800px-Olympic_swimming_pool_%28Tbilisi%29.jpg",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "swim@test.com",
    },
  ];
  function addMeetup() {
    const newMeetup = {
        id: Math.random().toString(),
        title: title,
        subtitle: subtitle,
        description: description,
        imageUrl: imageUrl,
        contactEmail: email,
        address: address
    }
    meetups = [newMeetup, ...meetups]
    }

    function toggleFavorite() {
      
    }
</script>

<Header />
<!-- <section id="meetups">
  {#each meetups as meetup, index (meetup.id)}
    <MeetupItem
      title={meetup.title}
      subtitle={meetup.subtitle}
      imageUrl={meetup.imageUrl}
      description={meetup.description}
      email={meetup.contactEmail}
      address={meetup.address}
    />
  {/each}
</section> -->



<!-- <main>
    <form on:submit|preventDefault="{addMeetup}">
        <div class="form-control">
            <label for="title">Title</label>
            <input type="text" id="title" bind:value={title}>
        </div>
        <div class="form-control">
            <label for="subtitle">Subtitle</label>
            <input type="text" id="subtitle" bind:value={subtitle}>
        </div>
        <div class="form-control">
            <label for="address">Address</label>
            <input type="text" id="address" bind:value={address}>
        </div>
        <div class="form-control">
            <label for="imageUrl">Image URL</label>
            <input type="text" id="imageUrl" bind:value={imageUrl}>
        </div>
        <div class="form-control">
            <label for="title">E-Mail</label>
            <input type="email" id="email" bind:value={email}>
        </div>
        <div class="form-control">
            <label for="description">Description</label>
            <textarea rows="3" id="description"  bind:value={description}/>
        </div>
        <button type="submit">Save</button>
    </form>
    <MeetupGrid {meetups} />
</main> -->

<main>
    <form on:submit|preventDefault={addMeetup}>
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
        label="Address"
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
      <Button type="submit" caption="Save"/>
    </form>
    <MeetupGrid {meetups} on:togglefavorite={toggleFavorite}/>
  </main>

<style>
  /* #meetups {
    margin-top: 5rem;
  } */

  main {
    margin-top: 5rem;
  }

  form{
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>
