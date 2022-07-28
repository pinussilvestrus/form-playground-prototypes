<script>
	import Playground from './components/Playground.svelte';

	import schema from './resources/form.json';

	const data = {
      creditor: 'John Doe Company',
      amount: 456,
      invoiceNumber: 'C-123',
      approved: true,
      approvedBy: 'John Doe',
      mailto: [ 'regional-manager', 'approver' ],
      product: 'camunda-cloud',
      queriedDRIs: [
        {
          'label': 'John Doe',
          'value': 'johnDoe'
        },
        {
          'label': 'Anna Bell',
          'value': 'annaBell'
        },
        {
          'label': 'Nico Togin',
          'value': 'incognito'
        }
      ],
      tags: [ 'tag1', 'tag2', 'tag3' ],
      language: 'english'
    };
</script>

<div id="root">
	<main>
		<Playground 
			schema={schema} 
			data={data}
		/>
</div>

<style lang="scss">
	#root {
		height: 100%;
		width: 100%;
	}

	main {
		flex-grow: 1;
		flex: 1;
		height: 100%;
  	display: flex;
  	flex-direction: column;
	}
</style>