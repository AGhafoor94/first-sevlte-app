<script>
  import PageItem from "./PageItem.svelte";
  export let pages;
</script>

<style>
  section {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 1rem;
  }

  @media (min-width: 768px) {
    section {
      grid-template-columns: repeat(2, 1fr);
    }
  }
</style>

<section id="pages">
  {#each pages as item}
    <PageItem
      id={item.id}
      title={item.title}
      subtitle={item.subtitle}
      description={item.description}
      image={item.image} />
  {/each}
</section>
