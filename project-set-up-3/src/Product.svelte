<script>
  import { createEventDispatcher } from "svelte";
  // export let productTitle
  export let title;
  export let price;
  export let bestSeller = false;
  function clickHandler(e) {
    console.log("Clicked");
  }

  const dispatch = createEventDispatcher();
  function addToCart() {
    // dispatch('add-to-cart', ownData);
    dispatch("add-to-cart", { id: "p1" });
  }
</script>

<article>
  <h1>{title}</h1>
  <h2>${price}</h2>
  {#if bestSeller}
    <h3>Best Seller</h3>
  {/if}
  <!-- <button on:click="{clickHandler}">Add to Cart</button> -->
  <!-- <button on:click>Add to Cart</button>
    <button on:click>Delete</button> -->
  <button on:click={addToCart}>Add to Cart</button>
  <button
    on:click={() => {
      dispatch("delete", "p1");
    }}>Delete</button
  >
</article>
