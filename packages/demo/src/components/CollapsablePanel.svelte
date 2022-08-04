<script>
  import { afterUpdate } from 'svelte';

  import classNames from 'classnames';

  import UpIcon from '../resources/up-bar.svg';
  import DownIcon from '../resources/down-bar.svg';
  import LeftIcon from '../resources/left-bar.svg';
  import RightIcon from '../resources/right-bar.svg';

  let className = '';

  let open = false;
  const toggle = () => {
    open = !open;
    onToggle()
  }

  $: {
    open = shouldOpen;
  }

  export let title = '';
  export let collapseTo = '';
  export let shouldOpen = false;
  export let onToggle = () => {};
	export { className as class };
</script>

<style lang="scss">
  .collapsable-panel {

    flex-grow: 1;
    display: flex;
    flex-direction: column;

    border-top: solid 1px var(--color-grey-225-10-75);

    &.collapse-bottom {
      position: absolute;
      bottom: 0;
      width: 100%;
    }

    .collapsable-panel-title {
      background: var(--color-grey-225-10-95);
      border-bottom: solid 1px var(--color-grey-225-10-75);
      display: flex;
      position: relative;

      h1 {
        font-size: 1rem;
        margin: 0;
        line-height: 2em;
        padding: .1em .5em;
      }

      .actions {
        border-left: 1px solid var(--color-grey-225-10-85);
        padding-left: 2px;
        position: absolute;
        right: 4px;
        top: 2px;
      }
    }

    .collapsable-panel-content {
      flex: 1;
      overflow: auto;
    }

    &:not(.open) {
      .collapsable-panel-content {
        display: none;
      }
    }
  }
</style>

<div class={classNames(
  className, 
  'collapsable-panel', 
  { open },
  { 'collapse-bottom': collapseTo === 'bottom' },
  { 'collapse-right': collapseTo === 'right' }
  )}>
  <div class="collapsable-panel-title">
    <h1>{ title }</h1>

    {#if collapseTo !== 'none'}
      <div class="actions">
        <button title={ open ? 'Close' : 'Open' } class="action" on:click={ toggle }>
          {#if collapseTo === 'right' }
            { @html RightIcon }
          {:else}
            {#if open}
              { @html DownIcon }
            {:else}
              { @html UpIcon }
            {/if}
          {/if}
        </button>
      </div>
    {/if}
  </div>

  <div class="collapsable-panel-content">
    <slot></slot>
  </div>
</div>