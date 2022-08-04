<script>
  import LeftIcon from '../resources/left-bar.svg';

  export let onTogglePreview = () => {};
</script>

<style lang="scss">
    .preview-toggle {
      height: 100%;
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      background: var(--color-grey-225-10-95);
      display: flex;
      position: relative;

      .preview-toggle-title {
        height: 100%;
      }

      h1 {
        font-size: 1rem;
        width: 120px;
        margin-left: -50px;
        margin-top: 60px;
        padding: .12em .5em;
        transform: rotate(-90deg);
        -webkit-transform: rotate(90deg);
        -moz-transform: rotate(90deg);
        -ms-transform: rotate(90deg);
        -o-transform: rotate(90deg);
      }

      .actions {
        border-top: 1px solid var(--color-grey-225-10-85);
        padding-top: 2px;
        left: 2px;
        position: absolute;
        bottom: 2px;
      }
    }
</style>

<div class="preview-toggle">
  <div class="preview-toggle-title">
    <h1>Form Preview</h1>
  </div>
  <div class="actions">
    <button title="Open Preview" class="action" on:click={ onTogglePreview }>
      { @html LeftIcon }
    </button>
  </div>
</div>