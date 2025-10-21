<script>
	import { RpcProvider } from 'starknet';

    const cggRpcUrl = 'https://api.cartridge.gg/x/starknet/sepolia';
    const corsAnywhereUrl = `https://cors-anywhere.com/${cggRpcUrl}`;

	const cggProvider = new RpcProvider({
		nodeUrl: corsAnywhereUrl,
        headers: {
            'Authorization': 'Bearer ' + import.meta.env.VITE_CGG_API_KEY,
        }
	});

    let loading = $state(false);
	let blockNumber = $state(0);

    const getBlockNumber = async () => {
        loading = true;
        try {
            blockNumber = await cggProvider.getBlockNumber();
        } catch (error) {
            console.error(error);
        } finally {
            loading = false;
        }
    }
</script>

<h1>Starknet Sepolia RPC Provider test</h1>

<button onclick={getBlockNumber}>
    {#if loading}
        <span>Loading...</span>
    {:else}
        Get Block Number
    {/if}
</button>

<p>Block Number: {blockNumber}</p>
