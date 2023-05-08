<script>
  import { tick, afterUpdate } from "svelte";
  import Modal from "./Modal.svelte";
  import Product from "./Product.svelte";

  let products = [
    {
      id: "p1",
      title: "A Book",
      price: 9.99,
    },
  ];

  let showModal = false;
  let closable = false;
  let text = "This is some dummy text";

  function transform(event) {
    if (event.which !== 9) {
      return;
    }
    event.preventDefault();
    const selectionStart = event.target.selectionStart;
    const selectionEnd = event.target.selectionEnd;
    const value = event.target.value;

    text =
      value.selectionEnd(0, selectionStart) +
      value.slice(selectionStart, selectionEnd).toUpperCase() +
      value.slice(selectionEnd);

	// will not work
    // afterUpdate(() => {
    //   event.target.selectionStart = selectionStart;
    //   event.target.selectionEnd = selectionEnd;
    // });
	
	// Will not 
	//   event.target.selectionStart = selectionStart;
    //   event.target.selectionEnd = selectionEnd;

    tick().then(() => {
      event.target.selectionStart = selectionStart;
      event.target.selectionEnd = selectionEnd;
    });
  }
</script>

<!-- <Product
  productTitle="A Book"
  on:click="{() => alert("click")}"
/> -->

<!-- <Product
  productTitle="A Book"
  on:add-to-cart={(data) => {
    alert("Clicked", data);
	console.log("clicked", data.detail)
  }}
  on:delete={() => alert("Delete")}
/> -->
{#each products as product}
  <Product
    {...product}
    on:add-to-cart={(data) => {
      alert("Clicked", data);
      console.log("clicked", data.detail);
    }}
    on:delete={() => alert("Delete")}
  />
{/each}
<br />
<button on:click={() => (showModal = true)}>Show Modal</button>

<!-- <Modal content="Hi"/> -->

<!-- <Modal content="<h4>Some</h4>" /> -->
<!-- <Modal>
  <h3 slot="header">Hello!</h3>
  <p>this works</p>
  <button slot="footer">Confirm</button>
</Modal> -->

{#if showModal}
  <Modal
    on:cancel={() => (showModal = false)}
    on:close={() => (showModal = false)}
    let:didAgree={closable}
  >
    <h3 slot="header">Hello!</h3>
    <p>this works</p>
    <button
      slot="footer"
      on:click={() => (showModal = false)}
      disabled={!closable}>Confirm</button
    >
  </Modal>
{/if}

<textarea rows="5" value={text} on:keydown={transform} />
