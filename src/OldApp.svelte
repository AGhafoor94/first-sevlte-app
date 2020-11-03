<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  //This goes into the file we want to add custom events to

  const addToCart = () => {
    dispatch("addToCart", { id: 1 });
  };
  //Then on:click={addToCart}

  import ContactCard from "./ContactCard.svelte";
  let name = "";
  let jobTitle = "IT Admin";
  let description = "IT worker";
  let image = "";
  const randName = ["Me", "You"];
  let formState = "empty";
  let createdContact = [];
  $: uppercaseName = name.toUpperCase();

  $: console.log(name);

  const changeName = () => {
    let item = randName[Math.floor(Math.random() * randName.length)];
    name = item;
  };
  const revert = () => {
    name = "name";
  };
  const nameInput = ({ target }) => {
    name = target.value;
  };
  const addContact = () => {
    if (!name || !jobTitle || !description || !image) {
      formState = "invalid";
    } else {
      formState = "done";
      createdContact = [
        ...createdContact,
        {
          id: Math.random(),
          name,
          jobTitle,
          image,
          description,
        },
      ];
      console.log(createdContact);
      formState = "done";
    }
  };
  const deleteFirst = () => {
    createdContact = createdContact.slice(1);
  };
  const deleteLast = () => {
    createdContact = createdContact.slice(0, -1);
  };
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<main>
  <h1>Hello {uppercaseName}!</h1>
  <button on:click={changeName}>Change Name</button>
  <button on:click={revert}>Revert</button>
  <!--2 Way binding-->
  <input type="text" value={name} on:input={nameInput} />
  <!--2 Way binding shorthand-->
  <input type="text" bind:value={name} />
  <input type="text" bind:value={jobTitle} />
  <textarea rows="3" bind:value={description} />
  <!--Importing component-->
  <form id="form">
    <div class="form-control">
      <label for="userName">User Name</label>
      <input type="text" bind:value={name} id="userName" />
    </div>
    <div class="form-control">
      <label for="jobTitle">Job Title</label>
      <input type="text" bind:value={jobTitle} id="jobTitle" />
    </div>
    <div class="form-control">
      <label for="image">Image URL</label>
      <input type="text" bind:value={image} id="image" />
    </div>
    <div class="form-control">
      <label for="desc">Description</label>
      <textarea rows="3" bind:value={description} id="desc" />
    </div>
    <button type="submit" on:click|preventDefault={addContact}>Submit</button>
  </form>
  <button on:click|once={addContact}>Add Contact</button>
  <!--capture, passive, stopPropagation, preventDefault-->
  <button on:click={deleteFirst}>Delete First</button>
  <button on:click={deleteLast}>Delete Last</button>
  {#if formState === 'invalid'}
    <p>Invalid</p>
  {:else}
    <p>Enter it</p>
  {/if}
  {#each createdContact as item, index (item.id)}
    <h2>{index}</h2>
    <ContactCard
      name={item.name}
      jobTitle={item.jobTitle}
      description={item.description}
      image={item.image} />
  {:else}
    <p>Empty</p>
  {/each}
</main>
