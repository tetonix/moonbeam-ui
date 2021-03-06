# Moonbeam UI Proof of Concept

This is a proof of concept UI for Moonbeam.  It works in conjunction with and connects to Moonbeam (https://github.com/PureStake/moonbeam).

It demonstrates a simple decentralized exchange heavily inspired by Uniswap, employing the same x * y = k constant product automated market making formula that was originally suggested by Vitalik Buterin (https://ethresear.ch/t/improving-front-running-resistance-of-x-y-k-market-makers/1281).  The current proof of concept only has 1 trading pair, GLMR and Tokens.

There are two participants in the system.  The first are liquidity providers that fund the token pool that sits behind the exchange market.  Liquidity is provided by depositing equivalent values of each token into the exchange pair in the exchange market.  Providers are compensated for this contribution of capital by earning tokens through trading fees that are automatically collected.  The second participant are traders that trade on an exchange market.  Traders send in some amount of one of the token pair to the market, and they will get back an amount of the other token dictated by the constant product formula less the trading fee.

The purpose of this proof of concept was to have a tangible project to learn Rust, Substrate, and javascript.  And also to understand, explore, and learn how automated market making DeFi applications work.

The prototype is built using the substrate-ui-template which in turn is created with [Create React App](https://github.com/facebook/create-react-app)
and [Polkadot js API](https://polkadot.js.org/api/). 

## Installation

The code can be installed using [git](https://git-scm.com/) and [yarn](https://yarnpkg.com/).

```bash
# Clone the repository
git clone https://github.com/PureStake/moonbeam-ui
cd ./moonbeam-ui
```

```bash
yarn install
```

## Usage

You can start the project in development mode to connect to a locally running node

```bash
yarn start
```

You can also build the app in production mode,

```bash
yarn build
```
and open `build/index.html` in your favorite browser.

## Configuration

The app's configuration is stored in the `src/config` directory, with
`common.json` being loaded first, then the environment-specific json file,
and finally environment variables, with precedence.

* `development.json` affects the development environment
* `test.json` affects the test environment, triggered in `yarn test` command.
* `production.json` affects the production environment, triggered in
`yarn build` command.

Some environment variables are read and integrated in the template `config` object,
including:

* `REACT_APP_PROVIDER_SOCKET` overriding `config[PROVIDER_SOCKET]`
* `REACT_APP_DEVELOPMENT_KEYRING` overriding `config[DEVELOPMENT_KEYRING]`

More on [React environment variables](https://create-react-app.dev/docs/adding-custom-environment-variables).

When writing and deploying your own front end, you should configure:

* `CUSTOM_TYPES` in `src/config/common.json`. See
  [Extending types](https://polkadot.js.org/api/start/types.extend.html).
* `PROVIDER_SOCKET` in `src/config/production.json` pointing to your own
  deployed node.
* `DEVELOPMENT_KEYRING` in `src/config/common.json` be set to `false`.
  See [Keyring](https://polkadot.js.org/api/start/keyring.html).

## Moonbeam Proof of Concept UI Quickstart

To use the UI, you need to do the following:
* Build and start a Moonbeam node (https://github.com/PureStake/moonbeam)
* Build and start a Moonbeam UI with yarn start
* Point your browser at http://localhost:8000
* In order to start using the application, you need to set GLMR and Token balances for a user (e.g. Alice).  
* To do this, use the Sudo module from the polkadot-js apps ui, and call the setGlmrBalance and setTokenBalance functions.
* Once you have GLMR and TOKEN balances, you can deposit liquidity into the exchange.
* The very first liquidity deposit has to specify a number of both GLMR and Tokens.  Once there are reserves in the exchange, you only specify a GLMR amount.
* After depositing liquidity, you can try trading GLMR to TOKEN and TOKEN to GLMR.
* You can withdraw liquidity from the exchange at any time.
* NOTE: the underlying currency of this blockchain is GLMR, but I haven't wired up the GLMR you see in the app to the underlying currency system.  What this means is that e.g. the balance you see in the upper right hand corner next to the account selector is totally separate from and doesn't reflect the GLMR balances in the application.


