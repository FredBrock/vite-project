<script>
  import Popover from "../Popover.svelte";
  export let title;
</script>

<li>
  <Popover>
    <div slot="trigger">
      <slot name="title">{title}</slot>
    </div>

    <div slot="content">
      <ul>
        <slot></slot>
      </ul>
    </div>
  </Popover>
</li>

<style>
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
    border-radius: 4px;
    background-color: #fff;
    width: 125px !important;
    min-width: auto;
    padding: 10px 0 !important;
    border-radius: 4px !important;
  }
</style>
