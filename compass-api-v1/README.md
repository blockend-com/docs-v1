# Compass API V1

\
Compass API v1

Page actionsGetting StartedBase URL: https://api2.blockend.com/v1/ All type definitions can be foundhereAuthenticationWhile Blockend API can be accessed without authentication, it is recommended to authenticate to get access to more features and higher rate limits.To authenticate, you need to pass in the api-key in the request header.const headers = {'x-api-key': 'YOUR\_API\_KEY'};​fetch('https://api2.blockend.com/v1/tokens', { headers }).then(response => response.json()).then(data => console.log(data));Commentcurl -X GET "https://api2.blockend.com/v1/tokens" \\-H "x-api-key: YOUR\_API\_KEY"Comment

### Rate Limiting <a href="#rate-limiting" id="rate-limiting"></a>

CommentWithout authentication, users can make up to 20 requests per minute. Users are counted on the basis of their IP address.CommentThere are no rate limits for authenticated users. Tho fare usage policy applies.Comment

### Steps <a href="#steps" id="steps"></a>

Comment

#### 1. Fetching quotes <a href="#id-1.-fetching-quotes" id="id-1.-fetching-quotes"></a>

CommentUser flow begins with fetching quotes, which returns a list of quotes for the given input and output assets, along with the steps involved in the transaction. Quotes are by default sorted via best output and contains a scores object and tags to determin fastest/cheapest/best output routes.Comment​[Get Quotes Documentation](https://app.gitbook.com/o/IeREEUPPPAY3j5XgVV5H/s/HWEUvrIp91EFDfyRl7CC/get-quotes)​Comment

#### 2. Creating a transaction <a href="#id-2.-creating-a-transaction" id="id-2.-creating-a-transaction"></a>

CommentAfter fetching quotes, you can create a transaction using the selected quote by passing in the `routeId` of the quote.Comment​[Create Transaction Documentation](https://app.gitbook.com/o/IeREEUPPPAY3j5XgVV5H/s/HWEUvrIp91EFDfyRl7CC/create-txn)​Comment

#### 3. Getting transaction data to execute <a href="#id-3.-getting-transaction-data-to-execute" id="id-3.-getting-transaction-data-to-execute"></a>

CommentCall this api with `routeId` and `stepId` of individual steps to get the transaction data to execute.Comment​[Get Transaction Data Documentation](https://app.gitbook.com/o/IeREEUPPPAY3j5XgVV5H/s/HWEUvrIp91EFDfyRl7CC/next-txn)​Comment

#### 4. Check status of a transaction <a href="#id-4.-check-status-of-a-transaction" id="id-4.-check-status-of-a-transaction"></a>

CommentAfter user signs and submits the transaction on chain, check the status of the transaction by passing in the signature hash of the transaction.Comment​[Check Transaction Status Documentation](https://app.gitbook.com/o/IeREEUPPPAY3j5XgVV5H/s/HWEUvrIp91EFDfyRl7CC/status-check)​Comment

#### 5. Using WebSockets for realtime updates <a href="#id-5.-using-websockets-for-realtime-updates" id="id-5.-using-websockets-for-realtime-updates"></a>

CommentYou can also check the status of a transaction using WebSockets. This can provide faster and almost realtime updates on the status of a transaction.Comment

> Note: this feature is in active development and will be generally available soon. Contact us to get access to this feature.Comment

### Meta Endpoints <a href="#meta-endpoints" id="meta-endpoints"></a>

Comment

#### Tokens <a href="#tokens" id="tokens"></a>

CommentGet a list of supported tokens and their details.Commentcurl -X GET "https://api.blockend.com/v1/tokens?chainId=sol"Comment

#### Chains <a href="#chains" id="chains"></a>

CommentGet a list of supported chains and their details.Commentcurl -X GET "https://api.blockend.com/v1/chains"[\
](https://docs.blockend.com/api-docs)
