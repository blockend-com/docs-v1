# Supported Tokens

### &#x20;<a href="#supported-tokens" id="supported-tokens"></a>

Blockend Widget supports a whole array of token which would be difficult to list here, so we have built a handy API just for that

Copy

```
curl -X GET "https://api.blockend.com/v1/tokens" \
  -H "accept: application/json"
```

You can also pass `chainId` as query parameter to get tokens for a specific chain

Copy

```
curl -X GET "https://api.blockend.com/v1/tokens?chainId=sol" \
  -H "accept: application/json"
```

You can also get list of supported chains by calling the following endpoint

Copy

```
curl -X GET "https://api.blockend.com/v1/chains" \
  -H "accept: application/json"
```
