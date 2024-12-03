<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";
  import Popover from "./lib/Popover.svelte";
  import Menu from "./lib/menu/Menu.svelte";
</script>

<main>
  <!-- <Counter />
  <Popover></Popover> -->

  <Popover>
    <div slot="trigger">
      <img src={svelteLogo} class="logo" alt="Svelte logo" />
    </div>
    <div slot="content">
      <Menu></Menu>

      <img src={viteLogo} class="logo" alt="Vite logo" />
    </div>
  </Popover>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
