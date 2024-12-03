<script>
  import SubMenu from "./SubMenu.svelte";
</script>

<ul>
  <li>
    <SubMenu title="hello">
      <ul>
        <li>1</li>
        <li>2</li>
        <li>
          3

          <SubMenu title="hello2">
            <ul>
              <li>1-1</li>
              <li>2-1</li>
              <li>3-1</li>
            </ul>
          </SubMenu>
        </li>
      </ul>
    </SubMenu>
  </li>
</ul>

<style>
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
</style>
