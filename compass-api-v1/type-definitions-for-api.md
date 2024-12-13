# Type Definitions for API

##

#### Basic Types <a href="#basic-types" id="basic-types"></a>

Copy

```
type NetworkType = "evm" | "sol" | "utxo" | "cosmos" | "tron";

type Asset = {
  networkType?: NetworkType;
  chainId: string;
  address: string;
  decimals: number;

  symbol: string;
  name?: string;
  isNative?: boolean;
  isPopular?: boolean;
  image?: string;

  blockchain: string;
  lastPrice: number;
  marketCap?: number;
};

type Chain = {
  chainId: string;
  symbol: string;
  name: string;
  networkType: NetworkType;

  image: string;
  isPopular?: boolean;
  isEnabled: boolean;

  explorer: {
    token: string; // https://polygonscan.com/token/{tokenAddress}
    txn: string; // https://polygonscan.com/tx/{txnHash}
    address?: string; // https://polygonscan.com/address/{address}
  };
  rpcUrls: string[];
  tokenCount: number;
};

enum FeeType {
  NETWORK = "NETWORK", // gas fee
  PROVIDER = "PROVIDER", // fee charged by the provider
  BLOCKEND = "BLOCKEND", // fee charged by blockend
  INTEGRATOR = "INTEGRATOR", // custom fee someone want to charge via blockend integration
};

enum FeeSource {
  FROM_SOURCE_WALLET = "FROM_SOURCE_WALLET", // fee charged on top of input amount
  FROM_OUTPUT_AMOUNT = "FROM_OUTPUT_AMOUNT", // fee ajusted in output amount
};

type ProviderDetails = {
  name: string;
  logoUrl: string;
};

type StepType = "approval" | "swap" | "bridge" | "sign" | "claim";
type TxnStatus = "not-started" | "in-progress" | "success" | "failed" | "cancelled";
```

#### Get Quotes <a href="#get-quotes" id="get-quotes"></a>

Copy

```
type QuoteRequest = {
  fromChainId: string; // chainId of the asset to swap from
  fromAssetAddress: string; // address of the asset to swap from

  toChainId: string; // chainId of the asset to swap to
  toAssetAddress: string; // address of the asset to swap to

  // send either inputAmountDisplay or inputAmount
  inputAmountDisplay: string; // 3.2
  inputAmount: string; // 3.2*10^18

  userWalletAddress: string; // address of the user who will perform the swap
  recipient?: string; // address of the recipient (in case, user is not the recipient)
};

type QuoteResponse = {
  quotes: Quote[];
};

type Quote = {
  requestId?: string;
  routeId: string;

  from: Asset;
  to: Asset;
  steps: Steps[];
  fee: Fee[];

  provider: Providers;
  providerDetails: ProviderDetails;
  protocolsUsed: string[];

  inputAmount: string; // 3.2*10^18
  inputAmountDisplay: string; // 3.2

  outputAmount: string; // 4.56*10^18
  outputAmountDisplay: string; // 4.56
  minOutputAmount: string; // 4.32*10^18
  minOutputAmountDisplay?: string; // 4.32
  slippage: number;

  userWalletAddress: string;
  recipient?: string;

  // time when quote is created (fetched) from provider
  // can also be used for removing old unused quotes
  createdAt: number;
  deadline: number; // deadline (in seconds) for quote to be used
  estimatedTimeInSeconds: number;

  isActive?: boolean; // set when quote is used (create txn)
  status?: TxnStatus;
  points?: number;

  warnings?: string[];
  tags?: string[];
  score?: any;
};

type Steps = {
  stepId: string;
  stepType: StepType;
  protocolsUsed: string[];
  provider?: Providers;

  from: Asset;
  to: Asset;
  txnHash?: string;
  status?: TxnStatus;

  inputAmount: string;
  outputAmount: string;
  fee: Fee[];
  estimatedTimeInSeconds?: number;

  texts?: {
    heading: string;

    preText: string;
    loadingText: string;
    postText: string;

    preDescription: string;
    preCta: string;
    processingDescription: string;
    processingCta: string;

    status: {
      pending: string;
      success: string;
      failed: string;
    }
  };
};

type Fee = {
  type: FeeType;
  amount: string; // currently same as amountInEther field
  amountInEther: string; // amount of fee to be paid token
  amountInUSD: string; // equivalent amount in USD
  token: Asset;
};
```

#### Create a transaction <a href="#create-a-transaction" id="create-a-transaction"></a>

Copy

```

type CreateTxnRequest = {
  routeId: string;
};

type CreateTxnResponse = {
  routeId: string;
  steps: Steps[];
};
```

#### Next step in a transaction <a href="#next-step-in-a-transaction" id="next-step-in-a-transaction"></a>

Copy

```
type NextTxnRequest = {
  routeId: string;
  stepId: string;
};

type NextTxnResponse = {
  routeId: string;
  stepId: string;
  txnData: TxnData | null;
  skipTxn?: boolean;
};

type TxnData = TxnMetaData & {
  txnEvm?: TxnEvm;
  txnSol?: TxnSol;
  txnTron?: TxnTron;
};

type TxnEvm = {
  from: string | null;
  to: string;
  value?: string | null;
  data?: string | null;
};

type TxnSol = {
  data: string;
};

type TxnTron = {
  raw_data?: any | null;
  raw_data_dex?: string | null;
  txID: string;
  visible: boolean;
};

type TxnMetaData = {
  id: string; // or can be simple step number
  requestId?: string;
  routeId: string;
  stepId: string;

  isCompleted: boolean;
  deadline?: number;

  networkType: NetworkType;
  status?: TxnStatus;

  txnHash?: string;
  txnBlock?: string;
  txnStatus?: TxnStatus;
  srcTxnHash?: string;
  srcTxnUrl?: string;
  destTxnHash?: string;
  destTxnUrl?: string;
  txnData?: any;

  createdAt: number;
  fetchedAt?: number; // 1st time when txnData is fetched by user (/nextTxn endpoint)
  txnHashUpdatedAt?: number; // 1st time when txnHash is submitted by user (/status check endpoint)
  srcHashConfirmedAt?: number; // time when srcTxnHash is confirmed by BE
  destHashConfirmedAt?: number; // time when destTxnHash is confirmed by BE

  exchangeData?: any;
  skipTxn?: boolean;
  points?: number;
};
```

#### Check status of a transaction <a href="#check-status-of-a-transaction" id="check-status-of-a-transaction"></a>

Copy

```
type StatusCheckRequest = NextTxnRequest & {
  txnHash: string;
};

type StatusCheckResponse = {
  routeId: string;
  stepId: string;
  status: TxnStatus;
  srcTxnHash?: string;
  srcTxnUrl?: string;
  destTxnHash?: string;
  destTxnUrl?: string;
  points?: number;
};
```

[\
](https://docs.blockend.com/status-check)
