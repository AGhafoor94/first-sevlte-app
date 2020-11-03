<script>
  import PagesGrid from "./Pages/PagesGrid.svelte";
  import Header from "./UI/Header.svelte";
  import TextInput from "./UI/TextInput.svelte";

  let title = "";
  let subtitle = "";
  let description = "";
  let image = "";

  let pages = [
    {
      id: 1,
      title: "Page 1",
      subtitle: "subtitle",
      description: "description",
      image: "https://i.imgur.com/gt74EGw.jpg",
    },
    {
      id: 2,
      title: "Page 2",
      subtitle: "subtitle 2",
      description: "description",
      image: "https://i.imgur.com/mgfgDYb.jpg",
    },
  ];

  const addPage = ({ target }) => {
    const newPage = {
      id: Math.random(),
      title: target.title.value,
      subtitle: target.subtitle.value,
      description: target.description.value,
      image: target.image.value,
    };
    pages = [newPage, ...pages];
  };
</script>

<Header />
<main>
  <h1>Pages</h1>

  <form on:submit|preventDefault={addPage}>
    <TextInput
      id="title"
      label="Title"
      value={title}
      on:input={(event) => (title = event.target.title)} />
    <TextInput
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      on:input={(event) => (subtitle = event.target.subtitle)} />
    <TextInput
      controlType="textarea"
      id="description"
      label="Description"
      value={description}
      on:input={(event) => (description = event.target.description)} />
    <TextInput
      id="image"
      label="Image"
      value={image}
      on:input={(event) => (image = event.target.image)} />

    <button type="submit">Submit</button>
  </form>
  <PagesGrid {pages} />
</main>
