<script>
	import { RpcProvider } from 'starknet';

	const cggRpcUrl = 'https://api.cartridge.gg/x/starknet/sepolia';
	//const corsAnywhereUrl = `https://cors-anywhere.com/${cggRpcUrl}`;

	const cggProvider = new RpcProvider({
		nodeUrl: cggRpcUrl
	});

	let loading = $state(false);
	let blockNumber = $state(0);
	let rpcSpec = $state('');

	const getBlockNumber = async () => {
		loading = true;
		try {
			blockNumber = await cggProvider.getBlockNumber();
		} catch (error) {
			console.error(error);
		} finally {
			loading = false;
		}
	};

    const getRpcSpec = async () => {
        loading = true;
        try {
            rpcSpec = await cggProvider.getSpecVersion();
        } catch (error) {
            console.error(error);
        } finally {
            loading = false;
        }
    };
</script>

<h1>Starknet Sepolia RPC Provider test</h1>

<div>
	<button onclick={getBlockNumber}>
		{#if loading}
			<span>Loading...</span>
		{:else}
			Get Block Number
		{/if}
	</button>

	<p>Block Number: {blockNumber}</p>
</div>


<div>
	<button onclick={getRpcSpec}>
		{#if loading}
			<span>Loading...</span>
		{:else}
			Get RPC Spec
		{/if}
	</button>

	<p>RPC Spec: {rpcSpec}</p>    
</div>
