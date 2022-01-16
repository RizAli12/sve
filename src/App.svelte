<script>
  let html = "<p>Write some text!</p>";

  let value = `Some words are *italic*, some are **bold**`;

  let scoops = 1;
  let flavours = ["Mint choc chip"];

  let menu = ["Cookies and cream", "Mint choc chip", "Raspberry ripple"];

  function join(flavours) {
    if (flavours.length === 1) return flavours[0];
    return `${flavours.slice(0, -1).join(", ")} and ${
      flavours[flavours.length - 1]
    }`;
  }

  let questions = [
    { id: 1, text: `Where did you go to school?` },
    { id: 2, text: `What is your mother's name?` },
    {
      id: 3,
      text: `What is another personal fact that an attacker could easily find with Google?`,
    },
  ];

  let selected;

  let answer = "";

  function handleSubmit() {
    alert(
      `answered question ${selected.id} (${selected.text}) with "${answer}"`
    );
  }

  let yes = false;

  let a = 1;
  let b = 2;

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

  <h2>Insecurity questions</h2>

  <form on:submit|preventDefault={handleSubmit}>
    <select bind:value={selected} on:change={() => (answer = "")}>
      {#each questions as question}
        <option value={question}>
          {question.text}
        </option>
      {/each}
    </select>

    <input bind:value={answer} />

    <button disabled={!answer} type="submit"> Submit </button>
  </form>

  <p>selected question {selected ? selected.id : "[waiting...]"}</p>

  <label>
    <input type="number" bind:value={a} min="0" max="10" />
    <input type="range" bind:value={a} min="0" max="10" />
  </label>

  <label>
    <input type="number" bind:value={b} min="0" max="10" />
    <input type="range" bind:value={b} min="0" max="10" />
  </label>

  <p>{a} + {b} = {a + b}</p>

  <h3>Select your ICECREAM</h3>

  <h2>Size</h2>

  <label>
    <input type="radio" bind:group={scoops} value={1} />
    One scoop
  </label>

  <label>
    <input type="radio" bind:group={scoops} value={2} />
    Two scoops
  </label>

  <label>
    <input type="radio" bind:group={scoops} value={3} />
    Three scoops
  </label>

  <h2>Flavours</h2>

  <select multiple bind:value={flavours}>
    {#each menu as flavour}
      <option value={flavour}>
        {flavour}
      </option>
    {/each}
  </select>

  {#if flavours.length === 0}
    <p>Please select at least one flavour</p>
  {:else if flavours.length > scoops}
    <p>Can't order more flavours than scoops!</p>
  {:else}
    <p>
      You ordered {scoops}
      {scoops === 1 ? "scoop" : "scoops"}
      of {join(flavours)}
    </p>
  {/if}

  <label>
    <input type="checkbox" bind:checked={yes} />
    Yes! Send me regular email spam
  </label>

  {#if yes}
    <p>Thank you. We will bombard your inbox and sell your personal details.</p>
  {:else}
    <p>
      You must opt in to continue. If you're not paying, you're the product.
    </p>
  {/if}

  <button disabled={!yes}> Subscribe </button>

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

  <div contenteditable="true" bind:innerHTML={html} />

  <pre>{html}</pre>

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

  h3 {
    font-size: 3em;
    background-color: blueviolet;
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

  textarea {
    width: 100%;
    height: 200px;
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
  }
  div {
    background-color: #e75626;
    width: 100%;
    height: 100%;
  }

  label {
    display: flex;
    background-color: rgb(182, 226, 226);
  }
  input {
    margin: 6px;
  }

  input {
    max-width: 100%;
  }

  [contenteditable] {
    padding: 0.5em;
    border: 1px solid #eee;
    border-radius: 4px;
  }
</style>
