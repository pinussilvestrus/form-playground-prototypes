<script>
  import { onMount, afterUpdate } from 'svelte';

  import classNames from 'classnames';

  import { Playground } from '@bpmn-io/form-js-playground';

  import CollapsablePanel from './CollapsablePanel.svelte';
  import PreviewToggle from './PreviewToggle.svelte';

  import { shortcut } from '../hooks/useShortcut';

  import '@bpmn-io/form-js/dist/assets/form-js.css';
  import '@bpmn-io/form-js/dist/assets/form-js-editor.css';
  import '@bpmn-io/form-js/dist/assets/properties-panel.css';
  import '@bpmn-io/form-js/dist/assets/dragula.css';
  import '@bpmn-io/form-js-playground/dist/assets/form-js-playground.css';

  let editorContainer, formContainer, dataContainer, resultContainer;
  let paletteContainer, propertiesContainer;
  let playground;

  onMount(() => {
    playground = new Playground({
      data,
      schema,
      actions: { display: false },
      editor: { inlinePropertiesPanel: false },
      preview: { inline: false }
    });

    playground.on('playground.rendered', () => {
      playground.attachEditorContainer(editorContainer);
      playground.attachDataContainer(dataContainer);
      playground.attachPaletteContainer(paletteContainer);
      playground.attachPropertiesPanelContainer(propertiesContainer);
    })
  });

  afterUpdate(() => {
    if(previewOpen) {
      playground.attachPreviewContainer(formContainer);
      playground.attachResultContainer(resultContainer);
    }
  })

  let previewOpen = false;
  const onTogglePreview = () => {
    previewOpen = !previewOpen;
  };

  export let schema = {};
  export let data = {};
</script>

<style lang="scss">
  .playground {
    display: flex;
    overflow: hidden;
    flex: 1;

    position: relative;

    height: 100%;
    min-width: 720px;

    .main {
      display: flex;
      flex-direction: row;
      width: 100%;
      height: 100%;
    }

  }
</style>

<div class="playground" use:shortcut={{ control: true, code: 'KeyP', callback: onTogglePreview }}>

  <div bind:this={ paletteContainer } class="palette"></div>

  <div class={ classNames('main', { 'preview-open': previewOpen })}>
    <div class="left">

      <CollapsablePanel collapseTo="none" title="Form Definition" class="editor-container" shouldOpen={ true }>
        <div bind:this={ editorContainer }></div>
      </CollapsablePanel>
  
      <CollapsablePanel collapseTo="bottom" title="Form Input" class="data-container" shouldOpen={previewOpen}>
        <div bind:this={ dataContainer }></div>
      </CollapsablePanel>
    </div>
  
    <div class="right"> 
      {#if previewOpen}
        <CollapsablePanel collapseTo="right" title="Form Preview" class="form-container" shouldOpen={previewOpen} onToggle={ onTogglePreview }>
          <div bind:this={ formContainer }></div>
        </CollapsablePanel>
    
        <CollapsablePanel collapseTo="bottom" title="Form Output" shouldOpen={previewOpen} class="result-container">
          <div bind:this={ resultContainer }></div>
        </CollapsablePanel>
      {:else} 
        <PreviewToggle onTogglePreview={ onTogglePreview } />
      {/if}
    </div>
  </div>

  <div bind:this={ propertiesContainer } class="properties-panel"></div>
</div>