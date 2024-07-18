## Getting quotes
Flow starts with getting quotes for a transaction.
<br>  

Endpoint: `GET /quotes`  
Request query params
```url
/quotes
    ?fromChainId=
    &fromAssetAddress=
    &toChainId=
    &toAssetAddress=
    &inputAmountDisplay=
    &userWalletAddress=
    &recipient=
```

Reponse:
```typescript
{
    "quotes": Quote[];
}
```
<br>

### Example
The following exmaple shows how to get quotes for a cross-chain swap transaction from Ethereum to Solana. We'll be fetching quotes for ETH on Ethereum to USDC on Solana.  
<br>  

**Request:**
```url
https://api2.blockend.com/v1/quotes
    ?fromChainId=1
    &fromAssetAddress=0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
    &toChainId=sol
    &toAssetAddress=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v
    &inputAmountDisplay=0.420
    &userWalletAddress=0x17e7c3DD600529F34eFA1310f00996709FfA8d5c
    &recipient=7zSa114U45nJ8b8ALsuhszS2Kxto8grgedh65Q7xJYii
```
<br>  

**Response:**
```json
{
    "status": "success",
    "data": {
        "quotes": [
            {
                "routeId": "01J2WB1NY6MD3F25CJTTB01D8F",
                "from": {
                    "networkType": "evm",
                    "chainId": "1",
                    "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                    "decimals": 18,
                    "name": "Ethereum",
                    "symbol": "ETH",
                    "isNative": true,
                    "isPopular": true,
                    "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                    "priceId": "ethereum",
                    "blockchain": "Ethereum",
                    "lastPrice": 3480.62
                },
                "to": {
                    "symbol": "USDC",
                    "image": "https://assets.coingecko.com/coins/images/6319/small/usdc.png",
                    "priceId": "usd-coin",
                    "blockchain": "Solana",
                    "decimals": 6,
                    "address": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
                    "networkType": "sol",
                    "isNative": false,
                    "isPopular": false,
                    "chainId": "sol",
                    "name": "USDC",
                    "lastPrice": 1.002
                },
                "steps": [
                    {
                        "stepId": "01J2WB1NY64MKVCM8FM994WMZV",
                        "stepType": "bridge",
                        "protocolsUsed": [
                            "Auction"
                        ],
                        "provider": "mayan",
                        "from": {
                            "networkType": "evm",
                            "chainId": "1",
                            "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                            "decimals": 18,
                            "name": "Ethereum",
                            "symbol": "ETH",
                            "isNative": true,
                            "isPopular": true,
                            "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                            "priceId": "ethereum",
                            "blockchain": "Ethereum",
                            "lastPrice": 3480.62
                        },
                        "to": {
                            "symbol": "USDC",
                            "image": "https://assets.coingecko.com/coins/images/6319/small/usdc.png",
                            "priceId": "usd-coin",
                            "blockchain": "Solana",
                            "decimals": 6,
                            "address": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
                            "networkType": "sol",
                            "isNative": false,
                            "isPopular": false,
                            "chainId": "sol",
                            "name": "USDC",
                            "lastPrice": 1.002
                        },
                        "fee": [
                            {
                                "token": {
                                    "networkType": "evm",
                                    "chainId": "1",
                                    "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                                    "decimals": 18,
                                    "name": "Ethereum",
                                    "symbol": "ETH",
                                    "isNative": true,
                                    "isPopular": true,
                                    "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                                    "priceId": "ethereum",
                                    "blockchain": "Ethereum",
                                    "lastPrice": 3480.62
                                },
                                "amount": "1380475027400000",
                                "amountInEther": "1380475027400000",
                                "amountInUSD": "4.804908989868988",
                                "type": "network"
                            }
                        ],
                        "inputAmount": "420000000000000000",
                        "outputAmount": "1459244847",
                        "estimatedTimeInSeconds": 900
                    }
                ],
                "fee": [
                    {
                        "token": {
                            "networkType": "evm",
                            "chainId": "1",
                            "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                            "decimals": 18,
                            "name": "Ethereum",
                            "symbol": "ETH",
                            "isNative": true,
                            "isPopular": true,
                            "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                            "priceId": "ethereum",
                            "blockchain": "Ethereum",
                            "lastPrice": 3480.62
                        },
                        "amount": "1380475027400000",
                        "amountInEther": "1380475027400000",
                        "amountInUSD": "4.804908989868988",
                        "type": "network"
                    }
                ],
                "provider": "mayan",
                "providerDetails": {
                    "id": "mayan",
                    "name": "Mayan",
                    "logoUrl": "https://blockend-widget.s3.ap-south-1.amazonaws.com/mayan.svg",
                    "websiteUrl": "https://mayan.finance/"
                },
                "protocolsUsed": [
                    "Auction"
                ],
                "inputAmount": "420000000000000000",
                "inputAmountDisplay": "0.420",
                "outputAmount": "1459244847",
                "outputAmountDisplay": "1459.244847",
                "minOutputAmount": "1459.098923",
                "minOutputAmountDisplay": "1459.098923",
                "slippage": 0,
                "recipient": "7zSa114U45nJ8b8ALsuhszS2Kxto8grgedh65Q7xJYii",
                "createdAt": 1721085515718,
                "deadline": 60,
                "estimatedTimeInSeconds": 900,
                "requestId": "01J2WB1K2D769PJRBMPNX1SKJT",
                "score": {
                    "outputScore": 1,
                    "speedScore": 0.0011111111111111111,
                    "feeScore": 1,
                    "slipparageScore": 0,
                    "stepScore": 1,
                    "outputDiffPercent": 0
                },
                "tags": [
                    "BEST_OUTPUT",
                    "CHEAP"
                ]
            },
            {
                "routeId": "01J2WB1MX7ZDHNB71GH3R52189",
                "from": {
                    "networkType": "evm",
                    "chainId": "1",
                    "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                    "decimals": 18,
                    "name": "Ethereum",
                    "symbol": "ETH",
                    "isNative": true,
                    "isPopular": true,
                    "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                    "priceId": "ethereum",
                    "blockchain": "Ethereum",
                    "lastPrice": 3480.62
                },
                "to": {
                    "symbol": "USDC",
                    "image": "https://assets.coingecko.com/coins/images/6319/small/usdc.png",
                    "priceId": "usd-coin",
                    "blockchain": "Solana",
                    "decimals": 6,
                    "address": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
                    "networkType": "sol",
                    "isNative": false,
                    "isPopular": false,
                    "chainId": "sol",
                    "name": "USDC",
                    "lastPrice": 1.002
                },
                "steps": [
                    {
                        "stepId": "01J2WB1MX7BJA7ZSN8K4KXF1VA",
                        "stepType": "bridge",
                        "protocolsUsed": [
                            "deBridge"
                        ],
                        "provider": "dln",
                        "from": {
                            "networkType": "evm",
                            "chainId": "1",
                            "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                            "decimals": 18,
                            "name": "Ethereum",
                            "symbol": "ETH",
                            "isNative": true,
                            "isPopular": true,
                            "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                            "priceId": "ethereum",
                            "blockchain": "Ethereum",
                            "lastPrice": 3480.62
                        },
                        "to": {
                            "symbol": "USDC",
                            "image": "https://assets.coingecko.com/coins/images/6319/small/usdc.png",
                            "priceId": "usd-coin",
                            "blockchain": "Solana",
                            "decimals": 6,
                            "address": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
                            "networkType": "sol",
                            "isNative": false,
                            "isPopular": false,
                            "chainId": "sol",
                            "name": "USDC",
                            "lastPrice": 1.002
                        },
                        "fee": [
                            {
                                "type": "network",
                                "token": {
                                    "networkType": "evm",
                                    "chainId": "1",
                                    "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                                    "decimals": 18,
                                    "name": "Ethereum",
                                    "symbol": "ETH",
                                    "isNative": true,
                                    "isPopular": true,
                                    "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                                    "priceId": "ethereum",
                                    "blockchain": "Ethereum",
                                    "lastPrice": 3480.62
                                },
                                "amount": "5141425082200000",
                                "amountInEther": "5141425082200000",
                                "amountInUSD": "17.895346969606965"
                            }
                        ],
                        "inputAmount": "420000000000000000",
                        "outputAmount": "1449243299",
                        "estimatedTimeInSeconds": 1
                    }
                ],
                "fee": [
                    {
                        "type": "network",
                        "token": {
                            "networkType": "evm",
                            "chainId": "1",
                            "address": "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",
                            "decimals": 18,
                            "name": "Ethereum",
                            "symbol": "ETH",
                            "isNative": true,
                            "isPopular": true,
                            "image": "https://assets.coingecko.com/coins/images/279/standard/ethereum.png?1595348880",
                            "priceId": "ethereum",
                            "blockchain": "Ethereum",
                            "lastPrice": 3480.62
                        },
                        "amount": "5141425082200000",
                        "amountInEther": "5141425082200000",
                        "amountInUSD": "17.895346969606965"
                    }
                ],
                "provider": "dln",
                "providerDetails": {
                    "id": "dln",
                    "name": "DLN",
                    "logoUrl": "https://dln.trade/assets/images/favicon/apple-touch-icon.png",
                    "websiteUrl": "https://dln.trade/"
                },
                "protocolsUsed": [
                    "deBridge"
                ],
                "inputAmount": "420000000000000000",
                "inputAmountDisplay": "0.420",
                "outputAmount": "1449243299",
                "outputAmountDisplay": "1449.243299",
                "minOutputAmount": "1449.243299",
                "minOutputAmountDisplay": "1449.243299",
                "slippage": 0.3,
                "recipient": "7zSa114U45nJ8b8ALsuhszS2Kxto8grgedh65Q7xJYii",
                "createdAt": 1721085514664,
                "deadline": 30,
                "estimatedTimeInSeconds": 1,
                "requestId": "01J2WB1K2D769PJRBMPNX1SKJT",
                "score": {
                    "outputScore": 0.9932454038279075,
                    "speedScore": 1,
                    "feeScore": 0.26850046540195793,
                    "slipparageScore": 0,
                    "stepScore": 1,
                    "outputDiffPercent": 0.00677748576178394
                },
                "tags": [
                    "BEST",
                    "FAST"
                ]
            }
        ]
    }
}
```
