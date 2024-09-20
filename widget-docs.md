# <div style="font-size: 50px; text-align: center;"> <img width="40px" src="https://beta.blockend.com/blockendfavicon.svg"> Blockend</div>

Blockend Widget is a single-line-of-code integration which enables dapps to access users liquidity from across tokens, chains, and networks giving dapps higher market penetration and in-turn allowing more people to access the world of crypto and decentralized apps.

## Installation

Blockend Widget is available as an [npm package](https://www.npmjs.com/package/blockend).

**npm:**

```sh
npm install blockend
```

**yarn:**

```sh
yarn add blockend
```

## Getting started with Blockend Widget

Integrating widget to your dapp or webiste is very easy. It takes a full 3 line of code to integrate and start using Blockend Widget, now that's a lot of work for a human dev.

### 1. Import Widget dependencies

In your react app, start by importing the Blockend Widget and its styles

```jsx
import Blockend from "blockend";
import "blockend/dist/main.css";
```

You may encounter Server Error... ReferenceError: self is not defined in your Next JS app,
this is because blockend requires web apis to work and the web apis are not available on the server side when next js renders a page, in order to avoid this you can start by importing the Blockend Widget like below

```jsx
import dynamic from "next/dynamic";
const Blockend = dynamic(() => import("blockend"), {
  ssr: false,
});
import "blockend/dist/main.css";
```

### 2. Initialize the Widget

Add the widget component to your app

```jsx
<Blockend />
```

### Integrator Id (Required)

Unique identifier assigned to each integration partner. It is used to track and manage various integrations within our system.Error will be thrown if this field is empty.

```jsx
const configuration = {
  integratorId:""
  ...
};
<Blockend  configuration={configuration} />
```

This id will be added in the request header of api calls that is made by the widget.

And that is it, you have successfully integrated the Blockend Widget.

### 3. (optional) Customizing the Widget

As an optional step, you can also customize the look and feel of the widget. This can be done by passing a configuration object as prop when initializing the widget.

```jsx
const configuration = {
    gradientStyle: {
    background: "linear-gradient(#E66465, #9198E5)",
    spinnerColor: "#E66465",
    stopColor: "#9198E5",
  },
  containerStyle:{
    background:"#000000",
    border:"1px solid #fff",
    boxShadow:"1px 1px 7px 5px rgb(255,255,255,0.1)" ,
  },
  theme:"light",
  customTheme: {
    text: {
      primary: "#808080",
      secondary: "rgba(128, 128, 128, 0.75)",
      placeholder: "#cccccc",
      success: "#49AD71",
      error: "#FD5868",
    },
    background: {
      container: "#FFFFFF",
      secondary: "#E9E9E9",
      card:"#FFFFFF",
      networkCard: "#F6F6F6",
      loaderbar: "#E9E9E9",
      coin:"#E0E0E0",
      rewards:"#eaeaeb33"
    },
    border: {
      primary: "#E0E0E0",
      inputHighlight: "#9FC966",
    },
    fontFamily:'"micro 5 charted"', sans-serif, lato;
    shadow: {
      boxShadow: "1px 1px 7px 5px rgb(255,255,255,0.1)",
    },
  },
};

<Blockend configuration={configuration} />;
```

Full list of configuration options can be found [here](#configuration-options)

## Configuration Options

### Customizing gradient colors

You can customize the gradient colors of the widget by passing `gradientStyle` object in configuration.

```jsx
const configuration = {
  gradientStyle: {
    background: "linear-gradient(#E66465, #9198E5)",
    spinnerColor: "#E66465",
    stopColor: "#9198E5",
  },
  ...
};
```

You can customize the theme of the widget by passing `customTheme` object in configuration.

```jsx
const configuration = {
  // containerStyle will override the styles written for the widget container, containerStyle accepts all the inline style properties.
  containerStyle:{
    background:"#000000", // changes the background color of the widget to black
    border:"1px solid #fff", //adds border to the widget container
    boxShadow:"1px 1px 7px 5px rgb(255,255,255,0.1)" // for adding desired shadow effect to the container.
  },
  theme:"light",  // light or dark, if custom theme is applied then custom theme will override light/dark theme
  customTheme: {
    text: {
      primary: "#808080", // primary color of the theme, this applies to headings, main text, svgs, etc..,
      secondary: "rgba(128, 128, 128, 0.75)",  //secondary color of the theme, this applies to secondary headings, network names, route info ,etc..,
      placeholder: "#cccccc",// to update  placeholder colors like input placeholder,date picker heading etc.,
      success: "#49AD71", // view all routes Higher output color
      error: "#FD5868", // error messages and lower output.
    },
    background: {
      container: "#FFFFFF", // can be used to update the bg color of the widget container, input amount container and routes container.
      secondary: "#E9E9E9", // can be used to update the table cell background on portfolio page.
      card:"#FFFFFF", //can be used to update the card color of the widget
      networkCard: "#F6F6F6", // used as background color for top main networks cards and transaction hash container in tokens section.
      loaderbar: "#E9E9E9", // loader bar color accross the widget.
      coin:"#E0E0E0", // used to update th default background color of the coin and chain icons.
      rewards:"#eaeaeb33" // can be used to update the rewards section background color on history page
    },
    border: {
      primary: "#E0E0E0",// primary border color of the widget, can be used to update the container border,border of coin and chain icons, cards border of the widget.
      inputHighlight: "#9FC966", //inputHighlight is used to update the border color of search tokens input field on select chains page when there are more than 0 results.
    },
    fontFamily:'"micro 5 charted"', sans-serif, lato; // can be used to update the font family of the widget to match the parent site, add the fonts to your site and just pass the font name to the widget.
    shadow: {
      boxShadow: "1px 1px 7px 5px rgb(255,255,255,0.1)", // to add shadow effect to the container and cards.
    },
  },
};
```

### Setting Default Chains and Tokens

Widget gives you the option to set default chains and tokens to be shown to the user. This can be done by passing `defaultChains` and `defaultTokens` in configuration when initializing the widget.  
See list of [supported chains](#supported-chains) and [tokens](#supported-tokens) below.

```jsx
const configuration = {
  defaultChains: {
    from: { chainId: "10" }, // optimism
    to: { chainId: "sol" }, // solana
  },
  defaultTokens: {
    from: { tokenAddress: "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee" }, // eth on optimism
    to: { tokenAddress: "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v" }, // usdc on solana
  },
  ...
};
```

> Note: token address for native tokens is set to 0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee

<br>

Here is what a integration of widget on your frontend might look like:

```jsx
import Blockend from "blockend";
import "blockend/dist/main.css";

const configuration = {
  gradientStyle: {
    background: "linear-gradient(#e66465, #9198e5)",
    spinnerColor: "#e66465",
    stopColor: "#9198e5",
  },
  defaultChains: {
    from: { chainId: "10" }, // optimism
    to: { chainId: "sol" }, // solana
  },
  defaultTokens: {
    from: { tokenAddress: "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee" }, // eth on optimism
    to: { tokenAddress: "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v" }, // usdc on solana
  },
};

export const Home = () => {
  return <Blockend configuration={configuration} />;
};
```

## Supported Chains

| Chain         | Chain Id   |
| ------------- | ---------- |
| Solana        | sol        |
| Ethereum      | 1          |
| Optimism      | 10         |
| BSC           | 56         |
| Polygon       | 137        |
| FUSE          | 122        |
| Gnosis        | 100        |
| Fantom        | 250        |
| Base          | 8453       |
| Arbitrum      | 42161      |
| zkSync Era    | 324        |
| Polygon zkEVM | 1101       |
| Avalanche     | 43114      |
| Boba          | 288        |
| OKXChain      | 66         |
| Moonbeam      | 1284       |
| Moonriver     | 1285       |
| Cronos        | 25         |
| Heco          | 128        |
| Aurora        | 1313161554 |
| Harmony       | 1666600000 |
| Evmos         | 9001       |

## Supported Tokens

Blockend Widget supports a whole array of token which would be difficult to list here, so we have built a handy API just for that

```bash
curl -X GET "https://api.blockend.com/v1/tokens" \
  -H "accept: application/json"
```

<br>

You can also pass `chainId` as query parameter to get tokens for a specific chain

```bash
curl -X GET "https://api.blockend.com/v1/tokens?chainId=sol" \
  -H "accept: application/json"
```

<br>

You can also get list of supported chains by calling the following endpoint

```bash
curl -X GET "https://api.blockend.com/v1/chains" \
  -H "accept: application/json"
```

## Supported Integration Providers

While in beta we have integrated with a few providers, we are working on adding more providers to the list.

- [Mayan Finance](https://mayan.finance)
- [DLN (deBridge)](https://dln.trade)
- [Jupiter](https://jup.ag)
- [0x](https://0x.org)
- [LiFi](https://li.fi)
- [Socket](https://socket.tech)
- [1Inch](https://1inch.io)
- [Paraswap](https://paraswap.io)
