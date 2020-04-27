## Start Nes node
```shell
./nes --datadir=/yourdatadir --rpc --rpcapi=wallet,gbc,chainer,node,net,txpool
```

## 1. wallet_createAccount

* Request ( *replace your password and use a random id* )
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc":"2.0",
  "method":"wallet_createAccount",
  "params":["password"],
  "id":1
}
```
* Response
```json 
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88"
}
```

## 2. wallet_listAccounts

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc":"2.0",
  "method":"wallet_listAccounts",
  "params":[],
  "id":1
}
```

* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [
    "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
    "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88"
  ]
}
```
## 3. wallet_importRawKey

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "wallet_importRawKey",
  "params": [
    "1d1303c230ed5c7e6b1d3c5f6ed094ce169293f58bd715d8e5a1e50f1067f744", //hex private key
    "123456" //your password
  ],
  "id": 1
}
```
* Response
```json
{
	"jsonrpc": "2.0",
	"id": 1,
	"result": "Nsfb21597f88ff4908dd0609f53351f6d41a7a1625"
}
```

## 4. gbc_getBalance

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_getBalance",
  "params": [
    "Ns585b432ce83ea10bb1a4222838bbd385e87fc9eb",
    "latest" //"latest","earliest","pending" or block number
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x394c549ef8ef" //63000000002287 plk
}
```

## 5. gbc_estimatePower

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_estimatePower",
  "params": [
    {
      "from": "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
      "to": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88",
      "value": "0x8AC7230489E80000"
    }
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "result": "0x5208" //21000 plk
}
```

## 6. gbc_powerPrice

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_powerPrice",
  "params": [],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x3b9aca00" //1000000000 plk
}
```

## 7. gbc_getTransactionCount

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_getTransactionCount",
  "params": [
    "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
    "pending" //"latest" "earliest" or "pending"
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x13"
}
```

## 8. wallet_pushTransaction

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "wallet_pushTransaction",
  "params": [
    {
      "from": "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
      "to": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88",
      "value": "0x8AC7230489E80000", //plk
      "power": "0x5208",  //optional
      "powerPrice": "0x3B9ACA00",  //optional
      "data":"0x"  //optional
    },
    "123456" //your password(unlock account only within this call)
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x92c8f643dd46cf9c9bf1040cfc01993becc39f1d93f46abdc7cfa2c42bf7cab4" 
}
```

## 9. gbc_transactionOfHash

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_transactionOfHash",
  "params": [
    "0x92c8f643dd46cf9c9bf1040cfc01993becc39f1d93f46abdc7cfa2c42bf7cab4"
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0x1b7fc04161d91019c5ad42c3c903ae81fb1e15e31cfe2240218e6df165adaae5",
    "blockNumber": "0x3e19",
    "from": "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
    "power": "0x5208",
    "powerPrice": "0x3b9aca00",
    "hash": "0x92c8f643dd46cf9c9bf1040cfc01993becc39f1d93f46abdc7cfa2c42bf7cab4",
    "input": "0x",
    "nonce": "0x11",
    "to": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88",
    "transactionIndex": "0x0",
    "value": "0x8ac7230489e80000"
  }
}
```

## 10. gbc_getTransactionReceipt

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_getTransactionReceipt",
  "params": [
    "0x92c8f643dd46cf9c9bf1040cfc01993becc39f1d93f46abdc7cfa2c42bf7cab4"
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "status": "0x1", //1:success 0:failed
    "blockHash": "0x1b7fc04161d91019c5ad42c3c903ae81fb1e15e31cfe2240218e6df165adaae5",
    "blockNumber": "0x3e19",
    "contractAddress": null, 
    "cumulativePowerUsed": "0x5208",
    "from": "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
    "to": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88",
    "powerUsed": "0x5208",
    "logs": [],
    "logsBloom": "0x00...", //256 byte bloom filter
    "transactionHash": "0x92c8f643dd46cf9c9bf1040cfc01993becc39f1d93f46abdc7cfa2c42bf7cab4",
    "transactionIndex": "0x0"
  }
}
```

## 11. gbc_blockNumber

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_blockNumber",
  "params": [],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x410b"
}
```

## 12. gbc_syncing

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_syncing",
  "params": [],
  "id": 1
}
```
* Response

if not in sync

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": false
}
```
if syncing
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "currentBlock": "0x219",
    "highestBlock": "0x411d",
    "knownStates": "0x19",
    "pulledStates": "0x19",
    "startingBlock": "0x0"
  }
}
```

## 13. txpool_content

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "txpool_content",
  "params": [],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "pending": {
      "Ns72472A14fC44e77BE5c4c9Cd5E14CE7FEEf5f7BC": {
        "21": {
          "blockHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
          "blockNumber": null,
          "from": "Nse0d9eef7de9bb7e9e3025b4e2c2b86053e0aae77",
          "power": "0x5208",
          "powerPrice": "0x3b9aca00",
          "hash": "0x823f034174d3a4c413774c13851703f0cd6254d4b8fadc08eaa49ac816ec4fe9",
          "input": "0x",
          "nonce": "0x15",
          "to": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88",
          "transactionIndex": "0x0",
          "value": "0x8ac7230489e80000"
        }
      }
    },
    "queued": {}
  }
}
```

## 14. wallet_exportKeystore

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "wallet_exportKeystore",
  "params": [
    "Ns585b432ce83ea10bb1a4222838bbd385e87fc9eb",
    "123456" //your password
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hex": "0x7b2261...3a337d", //hex format 
    "json": "{\"address\":\"585b432ce83ea10bb1a4222838bbd385e87fc9eb\",\"crypto\":{\"cipher\":\"aes-128-ctr\",\"ciphertext\":\"3ae51f...a7eaff\",\"cipherparams\":{\"iv\":\"8ecddc...96a250\"},\"kdf\":\"scrypt\",\"kdfparams\":{\"dklen\":32,\"n\":262144,\"p\":1,\"r\":8,\"salt\":\"4df41a...ad2dbe\"},\"mac\":\"2f3a1d...24136d\"},\"id\":\"5c90f4ec-5b36-45ca-8839-fa1bccd963e5\",\"version\":3}" //json format 
  }
}
```

## 15. wallet_importKeystore

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "wallet_importKeystore",
  "params": [
    "0x7b2261......3a337d",  //hex format or json format string
    "123456" //your password
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "Ns585b432ce83ea10bb1a4222838bbd385e87fc9eb"
}
```

## 16. wallet_deleteAccount

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "wallet_deleteAccount",
  "params": [
    "Ns585b432ce83ea10bb1a4222838bbd385e87fc9eb",
    "123456" //your password
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": true
}
```

## [17. gbc_blockOfNumber](#17)

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_blockOfNumber",
  "params": [
    "0x31c9", //"earliest" "latest" "pending" or block number
    false //true: return tx info , false: return tx hash
  ],
  "id": 1
}
```
* Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "difficulty": "0x457529",
    "extraData": "0xd601836e657388676f312e31332e348777696e646f7773",
    "hash": "0x1b7fc04161d92019c5ad42c3c903ae81fb2e15e30cfe2240218e6df165adaae5",
    "logsBloom": "0x000000...000000",
    "miner": "Ns2b9fcf8425fc2c37993d025ab41fae332294fd88",
    "mixHash": "0x7acae53987e834891b768e562f33752fda3feec927e4bad87683499b8e709147",
    "nonce": "0x000000000007ba1e",
    "number": "0x3ec9",
    "parentHash": "0x1655b12376b42fe50df0bc174abdd73af1bb827d7b89ee2bc4b315f6a1b0e342",
    "powerLimit": "0x989680",
    "powerUsed": "0x5208",
    "receiptsRoot": "0x056b23fbba480696b65fe5a59b8f2148a1299103c4f57df839233af2cf4ca2d2",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "size": "0x289",
    "stateRoot": "0x53cf7cd8bd5163c1ee52984b7001eb2ff0804466d7ef42c1380621ff47dfe45e",
    "timestamp": "0x5ea26fb5",
    "totalDifficulty": "0xd79e54db6",
    "transactions": [
      "0x92c8f643dd46cf9c9bf1c40cfc01993becc39f0d91f46abdc7cfa2c42bf7cab4"
    ],
    "transactionsRoot": "0x4ae91a1d29bf4a17cc94ecbde15549115b1d4b4c98c6437a36a179a9a51600a2",
    "uncles": []
  }
}
```

## 18. gbc_blockOfHash

* Request
```json
POST: "http://127.0.0.1:9435/"
Header: "Content-Type: application/json; charset=utf-8"
Body: 
{
  "jsonrpc": "2.0",
  "method": "gbc_blockOfNumber",
  "params": [
    "0x1b7fc04161d92019c5ad42c3c903ae81fb2e15e30cfe2240218e6df165adaae5", 
    false //true: return tx info , false: return tx hash
  ],
  "id": 1
}
```

* Response
```
same as gbc_blockOfNumber
```

