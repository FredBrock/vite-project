<script>
  import { createCollapsible, melt } from '@melt-ui/svelte'
  const {
    elements: { root, content, trigger },
    states: { open }
  } = createCollapsible()
</script>
 
<div {...$root} use:root>
  <button {...$trigger} use:trigger>{$open ? 'Close' : 'Open'}</button>
  <div {...$content} use:content>Obi-Wan says: Hello there!</div>
</div>