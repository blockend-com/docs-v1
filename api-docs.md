# Blockend API v1

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://app.getpostman.com/run-collection/25193308-9db7ddc1-c22f-44f1-bcc4-badae4796dfb?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D25193308-9db7ddc1-c22f-44f1-bcc4-badae4796dfb%26entityType%3Dcollection%26workspaceId%3D996072e7-23dc-4dc5-abe3-a4351f3abba1)


## Getting Started
Base URL: `https://api2.blockend.com/v1/`  
All type definitions can be found [here](./types.md)  

## Authentication
While Blockend API can be accessed without authentication, it is recommended to authenticate to get access to more features and higher rate limits.

To authenticate, you need to pass in the api-key in the request header.

```js
const headers = {
    'x-api-key': 'YOUR_API_KEY'
};

fetch('https://api2.blockend.com/v1/tokens', { headers })
    .then(response => response.json())
    .then(data => console.log(data));
```

```bash
curl -X GET "https://api2.blockend.com/v1/tokens" \
    -H "x-api-key: YOUR_API_KEY"
```


## Rate Limiting
Without authentication, users can make up to 20 requests per minute.  
Users are counted on the basis of their IP address.

There are no rate limits for authenticated users. Tho fare usage policy applies.

## Steps

### 1. Fetching quotes
User flow begins with fetching quotes, which returns a list of quotes for the given input and output assets, along with the steps involved in the transaction.  
Quotes are by default sorted via best output and contains a scores object and tags to determin fastest/cheapest/best output routes.  

[Get Quotes Documentation](./get-quotes.md)

### 2. Creating a transaction
After fetching quotes, you can create a transaction using the selected quote by passing in the `routeId` of the quote.  

[Create Transaction Documentation](./create-txn.md)

### 3. Getting transaction data to execute
Call this api with `routeId` and `stepId` of individual steps to get the transaction data to execute.  

[Get Transaction Data Documentation](./next-txn.md)

### 4. Check status of a transaction
After user signs and submits the transaction on chain, check the status of the transaction by passing in the signature hash of the transaction.

[Check Transaction Status Documentation](./status-check.md)

### 5. Using WebSockets for realtime updates
You can also check the status of a transaction using WebSockets. This can provide faster and almost realtime updates on the status of a transaction.

> Note: this feature is in active development and will be generally available soon.  
> Contact us to get access to this feature.

## Meta Endpoints

### Tokens
Get a list of supported tokens and their details.  
```bash
curl -X GET "https://api.blockend.com/v1/tokens?chainId=sol"
```
### Chains
Get a list of supported chains and their details.  
```bash
curl -X GET "https://api.blockend.com/v1/chains"
```
