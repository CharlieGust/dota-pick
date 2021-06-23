<script lange ts>
  import { onMount } from "svelte";
  import { fly, fade } from "svelte/transition";
  import Button from "./Button.svelte";

  let unique = {};
  let heroes = [];
  let chosen = 0;
  let count = 0;
  let roles = [];

  onMount(async () => {
    const res = await fetch(`src/assets/heroes.json`);
    heroes = await res.json();
  });

  async function getRoles () {
    const res = await fetch(`src/assets/heroesRole.json`);
    roles = await res.json();


    // if(res.ok){
    //   return json;
    //   // let roller = JSON.stringify(json)}
    //  }else {
    //   throw new Error(json);
    // }
  }
  let isActive = false;

  let value = [];

   function getNew (newroles) {
     console.log(newroles)

     value = newroles;
     isActive = !isActive;
   }
    // if danmroles[0] === "Carry" {
    //   console.log{}
    // }
    // value = newRoles.roles[];
    // console.log()
 // }

  function choose() {
    getRoles();
    unique = {};
    chosen = Math.floor(Math.random() * 120 + 1);

  }

</script>
<Button>NM</Button>
<h1 class="title">RANDOM HERO GENERATOR</h1>
<div class="bigboy">
  <div class="danmboy">
    <div class="photos">
      {#each heroes as hero}
      <figure>
      <img src={hero.url_small_portrait} alt={hero.name} />
      </figure>
      {:else}
      <p>loading...</p>
      {/each}
    </div>
  </div>

  <div class="secondboy">
    <button class="btn" on:click={choose} on:click={() => (count += 1)}
      >Random hero</button>
    {#each heroes as hero}
    {#if chosen == hero.id}
    {#key unique}
    <div class="imgrandom"
      in:fly={{ x: -599, duration: 550, delay: 300 }}
      out:fly={{ y: 500, duration: 350 }}>
      <img src={hero.url_large_portrait} alt={hero.name} />
    </div>
    {/key}
      <div
      in:fly={{ x: -599, duration: 550, delay: 300 }}
      out:fly={{ y: 500, duration: 350 }}>
      {#each roles as role}
        {#if role.id == hero.id}
        <p style="text-transform:uppercase">{role.localized_name}</p>
        {#if role.primary_attr === "int"}
        <p style="color:blue; text-transform:uppercase">{role.primary_attr} - {role.attack_type}</p>
        {/if}
        {#if role.primary_attr === "str"}
        <p style="color:red; text-transform:uppercase">{role.primary_attr} - {role.attack_type}</p>
        {/if}
        {#if role.primary_attr === "agi"}
        <p style="color:green; text-transform:uppercase">{role.primary_attr} - {role.attack_type}</p>
        {/if}
        <!-- <p><button on:click={() => value = role.roles}>Visa roller</button></p> -->
        <button on:click={() => getNew(role.roles)}>Visa roller</button>
        {/if}
      {/each}
      </div>
    {/if}
    {/each}
    {#if isActive}
    <p>
    {#each value as item}
      <li id="liclass" transition:fade>{item}</li>
    {/each}
  </p>
    {/if}
  </div>
</div>
<style>
  :global(body) {
    background-color: #f0f0f0;
    color: #ed2121;
    transition: background-color 0.3s;
  }
  :global(body.dark-mode) {
    background-color: #1d3040;
    color: #ee7f29;
  }
  .title {
    font-size: 6vmin;
    font-family: "Courier New", Courier, monospace;
  }
  /* .counter {
    position: fixed;
    width: 8vmin;
    height: 8vmin;
    font-size: 5vmin;
    text-align: center;
    background-color: black;
    color: white;

  } */
  .bigboy {
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: center;
    top: 0;
    left: 0;
  }
  p {
    font-size: 2vmin;
  }
  .danmboy {
    flex-direction: column;
    width: 130vmin;
    height: 135vmin;
    border-bottom-width: 1vmin;
    border-right: solid 10px;
    padding: 0.5vmin;
    border-radius: 2vmin;
    padding: 1%;
  }
  .photos {
    display: grid;
    flex: 1;
    grid-template-columns: repeat(9, 1fr);
    grid-gap: 2vmin;
    margin: auto;
  }
  .secondboy {
    align-items: center;
    width: 50vmin;
    padding: 0.5vmin;
    margin-left: 2vmin;
    text-align: center;
  }
  #liclass {
    list-style-type: upper-roman;
    padding: none;
  }

  .btn {
    margin-bottom: 3vmin;
    margin-top: 3vmin;
    font-family: "Courier New", Courier, monospace;
    font-size: 5vmin;
    height: 6rem;
    width: 50vmin;
    background-color: #ed2121;
    color: white;
    border-radius: 2vmin;
    text-transform: uppercase;
    cursor: pointer;
  }
  :global(body.dark-mode) button {
    background-color: #ee7f29;
    color: white;
  }
  button {
      background-color: #ed2121;
      color: white;
      border: none;
      border-radius: 4px;
      padding: 0.5rem;
      text-transform: uppercase;
      cursor: pointer;
    }

  figure,
  img {
    margin: 0;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .imgrandom {
    height: 30vmin;
    width: 50vmin;
    border-radius: 2min;
  }
  img {
    width: 100%;
    height: 100%;
    border-radius: 1vmin;
  }
</style>
