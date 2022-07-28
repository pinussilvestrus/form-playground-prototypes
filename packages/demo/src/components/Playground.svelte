<script>
  import { onMount } from 'svelte';

  import { Playground } from '@bpmn-io/form-js-playground';

  import '@bpmn-io/form-js/dist/assets/form-js.css';
  import '@bpmn-io/form-js/dist/assets/form-js-editor.css';
  import '@bpmn-io/form-js/dist/assets/properties-panel.css';
  import '@bpmn-io/form-js/dist/assets/dragula.css';
  import '@bpmn-io/form-js-playground/dist/assets/form-js-playground.css';

  let container;

  onMount(async () => {
    const playground = new Playground({
      container,
      data,
      schema,
      propertiesPanel: { inline: false }
    });
  });

  export let schema = {};
  export let data = {};
</script>

<style lang="scss">
  #form {
    display: flex;
    flex: 1;

    position: relative;

    height: 100%;
    min-width: 720px;

    flex-direction: row;

    .form-container {
      flex: 1;
      position: relative;
    }
  }
</style>

<div id="form">
  <div bind:this={ container } class="form-container"></div>
</div>