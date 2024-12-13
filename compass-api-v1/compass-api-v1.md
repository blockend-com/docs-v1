# Compass API v1

### Getting Started <a href="#getting-started" id="getting-started"></a>

Base URL: `https://api2.blockend.com/v1/` All type definitions can be found [here](https://docs.blockend.com/types)

### Authentication <a href="#authentication" id="authentication"></a>

While Blockend API can be accessed without authentication, it is recommended to authenticate to get access to more features and higher rate limits.

To authenticate, you need to pass in the api-key in the request header.

Copy

```
const headers = {
    'x-api-key': 'YOUR_API_KEY'
};

fetch('https://api2.blockend.com/v1/tokens', { headers })
    .then(response => response.json())
    .then(data => console.log(data));
```

Copy

```
curl -X GET "https://api2.blockend.com/v1/tokens" \
    -H "x-api-key: YOUR_API_KEY"
```

### Rate Limiting <a href="#rate-limiting" id="rate-limiting"></a>

Without authentication, users can make up to 20 requests per minute. Users are counted on the basis of their IP address.

There are no rate limits for authenticated users. Tho fare usage policy applies.

### Steps <a href="#steps" id="steps"></a>

#### 1. Fetching quotes <a href="#id-1.-fetching-quotes" id="id-1.-fetching-quotes"></a>

User flow begins with fetching quotes, which returns a list of quotes for the given input and output assets, along with the steps involved in the transaction. Quotes are by default sorted via best output and contains a scores object and tags to determin fastest/cheapest/best output routes.

[Get Quotes Documentation](https://docs.blockend.com/get-quotes)

#### 2. Creating a transaction <a href="#id-2.-creating-a-transaction" id="id-2.-creating-a-transaction"></a>

After fetching quotes, you can create a transaction using the selected quote by passing in the `routeId` of the quote.

[Create Transaction Documentation](https://docs.blockend.com/create-txn)

#### 3. Getting transaction data to execute <a href="#id-3.-getting-transaction-data-to-execute" id="id-3.-getting-transaction-data-to-execute"></a>

Call this api with `routeId` and `stepId` of individual steps to get the transaction data to execute.

[Get Transaction Data Documentation](https://docs.blockend.com/next-txn)

#### 4. Check status of a transaction <a href="#id-4.-check-status-of-a-transaction" id="id-4.-check-status-of-a-transaction"></a>

After user signs and submits the transaction on chain, check the status of the transaction by passing in the signature hash of the transaction.

[Check Transaction Status Documentation](https://docs.blockend.com/status-check)

#### 5. Using WebSockets for realtime updates <a href="#id-5.-using-websockets-for-realtime-updates" id="id-5.-using-websockets-for-realtime-updates"></a>

You can also check the status of a transaction using WebSockets. This can provide faster and almost realtime updates on the status of a transaction.

> Note: this feature is in active development and will be generally available soon. Contact us to get access to this feature.

### Meta Endpoints <a href="#meta-endpoints" id="meta-endpoints"></a>

#### Tokens <a href="#tokens" id="tokens"></a>

Get a list of supported tokens and their details.

Copy

```
curl -X GET "https://api.blockend.com/v1/tokens?chainId=sol"
```

#### Chains <a href="#chains" id="chains"></a>

Get a list of supported chains and their details.

Copy

```
curl -X GET "https://api.blockend.com/v1/chains"
```
