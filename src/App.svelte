<script>
  import CustomButton from "./CustomButton.svelte";

  function handleClick01() {
    alert("Button Clicked");
  }

  let m = { x: 0, y: 0 };

  //DOM events

  function handleClick11() {
    alert("no more alerts");
  }

  import Inner from "./Inner.svelte";

  function handleMessage(event) {
    alert(event.detail.text);
  }

  //component-event

  import Info from "./Info.svelte";

  const pkg = {
    name: "svelte",
    version: 3,
    speed: "blazing",
    website: "https://svelte.dev",
  };

  async function getRandomNumber() {
    const res = await fetch(`/tutorial/random-number`);
    const text = await res.text();

    if (res.ok) {
      return text;
    } else {
      throw new Error(text);
    }
  }

  let promise = getRandomNumber();

  function handleClick02() {
    promise = getRandomNumber();
  }
  //await blocks

  let user = { loggedIn: false };

  function toggle() {
    user.loggedIn = !user.loggedIn;
  }

  import Nested from "./Nested.svelte";
  //Nested components

  let src = "image.GIF";
  //dynamic attributes

  let name = "world";
  let name2 = "Rick Astley";

  let string = `this string contains some <strong>HTML!!!</strong>`;
  //HTML tags

  let cats = [
    { id: "J---aiyznGQ", name: "Keyboard Cat" },
    { id: "z_AbfPXTKms", name: "Maru" },
    { id: "OUtn3pvWmpg", name: "Henri The Existential Cat" },
  ];

  //each block

  import Thing from "./Thing.svelte";

  let things = [
    { id: 1, name: "apple" },
    { id: 2, name: "banana" },
    { id: 3, name: "carrot" },
    { id: 4, name: "doughnut" },
    { id: 5, name: "egg" },
  ];

  function handleClick1() {
    things = things.slice(1);
  } //keyed each blocks

  let count = 0;
  function incrementCount() {
    count += 1;
  }

  //Assignments

  $: doubled = count * 2;

  $: if (count >= 10) {
    alert("count is dangerously high!");
    count = 9;
  }

  //Statments

  //Declarations

  let numbers = [1, 2, 3, 4];

  function addNumber() {
    numbers = [...numbers, numbers.length + 1];
  }

  $: sum = numbers.reduce((t, n) => t + n, 0);
  //Updating arrays and objects
</script>

<main>
  <Inner on:message={handleMessage} />
  {#if user.loggedIn}
    <button on:click={toggle}> Log out </button>
  {:else}
    <button on:click={toggle}> Log in </button>
  {/if}

  <input bind:value={name} />

  <h1>Hello {name}!</h1>

  <h1>Hello {name2.toUpperCase()}!</h1>

  <CustomButton on:click={handleClick01} />

  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
  <button on:click={handleClick02}> generate random number </button>
  {#await promise}
    <p>...waiting</p>
  {:then number}
    <p>The number is {number}</p>
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}

  <img {src} alt="{name2} dances." />

  <p>This is a paragraph.</p>

  <Nested answer={42} />
  <Nested />

  <button on:click={incrementCount}>
    Clicked {count}
    {count === 1 ? "time" : "times"}
  </button>
  {#if count > 10}
    <p>{count} is greater than 10</p>
  {:else if 5 > count}
    <p>{count} is less than 5</p>
  {:else}
    <p>{count} is between 5 and 10</p>
  {/if}

  <p>{count} doubled is {doubled}</p>

  <button on:click={addNumber}> Add a number </button>
  <p>{numbers.join(" + ")} = {sum}</p>

  <p>{@html string}</p>

  <div on:mousemove={(e) => (m = { x: e.clientX, y: e.clientY })}>
    The mouse position is {m.x} x {m.y}
  </div>

  <h2>The Famous Cats of YouTube</h2>

  <ul>
    {#each cats as { id, name }, i}
      <li>
        <a target="_blank" href="https://www.youtube.com/watch?v={id}">
          {i + 1}: {name}
        </a>
      </li>
    {/each}
  </ul>
  <button on:click|once={handleClick11}> Click me for Alert msg</button>
  <button on:click={handleClick1}> Remove first thing </button>

  {#each things as thing (thing.id)}
    <Thing name={thing.name} />
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    background-color: #c9c8c1;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  h2 {
    text-align: left;
    color: rgb(113, 140, 212);
  }
  ul {
    text-align: left;
    border-radius: 0.2em;
    background-color: #ffdfd3;
  }
  p {
    color: purple;
    font-family: "Comic Sans MS", cursive;
    font-size: 2em;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }

    div {
      background-color: #e75626;
      width: 100%;
      height: 100%;
    }
  }
</style>
