<script>
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'
  import IERC20 from '@openzeppelin/contracts/build/contracts/IERC20.json'

  import { onMount } from 'svelte'
  import { defaultEvmStores as evm, contracts, selectedAccount, chainId } from 'svelte-web3'
  onMount( evm.setProvider )

  evm.attachContract('link', '0x326C977E6efc84E512bB9C30f76E30c160eD06FB', IERC20.abi)

  selectedAccount.subscribe(async $a => {
    if (!$a) return

    console.log('connected to account ', $a)
  })

  contracts.subscribe(async $c => {
    if (!$c.link) return
    const total = await $contracts.link.methods.totalSupply().call()
    console.log('total is', total)
  })

</script>

<main>

  <p>account: {$selectedAccount} / chainId: {$chainId}</p>

  <div>
    <a href="https://vitejs.dev" target="_blank"> 
      <img src="/vite.svg" class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank"> 
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
