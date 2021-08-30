# Wallet

A Minimalistic ethereum based wallet powered by web3-react with a simple wallet modal.

## Getting Started

This package uses `@web3-react` under the  hood with a react modal to easily hook into any dapps, so first you need to install the following `peerDependencies` to use the package.

```
"web3": "^1.3.5",
"ethers": "^5.1.2",
"@web3-react/core": "^6.1.9",
"@web3-react/injected-connector": "^6.0.7",
"@web3-react/walletconnect-connector": "^6.2.4",
"@binance-chain/bsc-connector": "^1.0.0"

```

Copy paste the following dependencies into your package.json, dependencies section, and run `npm install`.  

    
To use the package, first you need to import the `WalletProvider` and place it at the top level in the component tree.

```

import { WalletProvider } from "@react-dapp/wallet";
...

ReactDOM.render(
  <React.StrictMode>
    <WalletProvider isBSC={true} chainId={42} isDarkMode={false}>
      ...
    </WalletProvider>
  </React.StrictMode>,
  document.getElementById("root")
);


```

> - `isBSC` prop will render the `Binance Wallet Button` if `true`.
> - Provide `chainId` of the network you wanna connect.
> - `isDarkMode` controls between dark and light theme of the modal.

<br/>  

To open wallet modal, use `uesWalletModal` hook

```

import { useWalletModal, useWeb3 } from "@react-dapp/wallet";
...

const Connect = ()=> {

    const { open, setOpen } = useWalletModal();
    const { account } = useWeb3();

    return (
        <Button onClick={() => setOpen(true)}>
          {account ? account.substring(0, 5) + "..." : "Connect"}
        </Button>
    )
}

```

To use the current **web3 provider** and connected **account** use `useWeb3` hook

```

const { account, web3 } = useWeb3();

```

Following are some of the useful hooks that can be helpful in many dapps.

### useLp
This is can be used to fetch info about the LP token used by pancake or similar exchanges.

```
@params: 
LpAddress: required,
baseTokenSymbol: optional, 
baseTokenAddress: optional

@returns
{
    loading,
    lp: {
        name,
        symbol,
        token0,
        token1,
    },
    token0: {
        name,
        symbol,
        decimals,
        address,
        totalSupply,
        lpBalance
    },
    token0: ...,
    price: {
        token0,
        token1,
        basePrice
    }

}
```

### useERC20Approval