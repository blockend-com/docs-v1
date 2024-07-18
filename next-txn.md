## Getting transaction data to execute
Call this api with `routeId` and `stepId` of individual steps to get the transaction data to execute.  
Once the transaction is executed, check the status of the transaction using `/status` api and proceed to the next step of the transaction.  
<br>  

> Note: you can ignore status check and skip to next step of the txn if `skipTxn` field is set to `true` in the response.  
> Also, when `skipTxn` is set to `true`, `txnData` will be `null`.

<br>  

Endpoint: `GET /nextTx`  
Request query params
```url
/nextTx?
    routeId=
    &stepId=
```

Response:
```typescript
{
    routeId: string;
    stepId: string;
    txnData: TxnData | null;
    skipTxn?: boolean;
}
```
<br>  

### Example
Lets now fetch the transaction data for the first step of the transaction we created in `/createTx` api.

**Request:**
```url
https://api2.blockend.com/v1/nextTx
    ?routeId=01J2WB2ZTWAWXN9K48899CSSVN
    &stepId=01J2WB3JEB34B0A1SXHT1E3B63
```
<br>  

**Response:**  
As the
```json
{
    "status": "success",
    "data": {
        "routeId": "01J2WB2ZTWAWXN9K48899CSSVN",
        "stepId": "01J2WB3JEB34B0A1SXHT1E3B63",
        "txnData": {
            "id": "01J2WD2YRTT6AN4450NKX9H1WB",
            "routeId": "01J2WB2ZTWAWXN9K48899CSSVN",
            "stepId": "01J2WB3JEB34B0A1SXHT1E3B63",
            "isCompleted": false,
            "networkType": "evm",
            "txnEvm": {
                "from": "0x17e7c3DD600529F34eFA1310f00996709FfA8d5c",
                "to": "0x3c499c542cef5e3811e1192ce70d8cc03d5c3359",
                "data": "0x095ea7b3000000000000000000000000ef4fb24ad0916217251f553c0596f8edc630eb66ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
                "gasPrice": "30000000030",
                "gasLimit": 56167
            },
            "createdAt": 1721087654682,
            "status": "not-started",
            "fetchedAt": 1721087654682,
            "requestId": "01J2WB2ZBWNW0M0CJEYV415HPZ"
        }
    }
}
```
