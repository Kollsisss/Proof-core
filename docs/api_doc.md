# Proof Blockchain: API Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Authentication](#authentication)
3. [Proof Key](#proof-key)
4. [Rate Limiting](#rate-limiting)
5. [API Endpoints](#api-endpoints)
   - [Account](#account)
   - [Transactions](#transactions)
   - [Blocks](#blocks)
   - [Smart Contracts](#smart-contracts)
   - [Network Statistics](#network-statistics)
6. [Error Handling](#error-handling)
7. [Websocket API](#websocket-api)
8. [Security Best Practices](#security-best-practices)
9. [Changelog](#changelog)

## 1. Introduction

Welcome to the Proof Blockchain API documentation. This API provides secure access to on-chain data and limited off-chain functionalities. It is designed to allow developers to interact with the Proof Blockchain network while maintaining the highest standards of security, data privacy, and transparency.

Base URL: `https://api.proof.blockchain/v1`

## 2. Authentication

All API requests must be authenticated using JWT (JSON Web Tokens).

To obtain a JWT:

1. Register for an API key at `https://developer.proof.blockchain`
2. Use your API key to request a JWT at the `/auth` endpoint

Example:

```bash
curl -X POST https://api.proof.blockchain/v1/auth \
  -H "Content-Type: application/json" \
  -d '{"apiKey": "your_api_key_here"}'
```

The response will contain your JWT, which you should include in the `Authorization` header of all subsequent requests:

```
Authorization: Bearer your_jwt_token_here
```

JWTs expire after 24 hours. You should request a new token before expiration.

## 3. Proof Key

To ensure transparency and accountability, all API requests that read or modify data must include the user's Proof Key. This key is used to log all data access attempts on the blockchain.

To include your Proof Key in a request, add it to the `X-Proof-Key` header:

```
X-Proof-Key: your_proof_key_here
```

Your Proof Key can be obtained from your Proof Blockchain wallet. Never share your Proof Key with others.

## 4. Rate Limiting

To ensure fair usage and protect the network, API requests are rate-limited:

- 100 requests per minute for standard users
- 1000 requests per minute for verified developers

Rate limit headers are included in all API responses:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1620000000
```

## 5. API Endpoints

### Account

#### Get Account Balance

```
GET /account/{address}/balance
```

Returns the current balance of the specified account address.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Parameters:
- `address`: The Proof Blockchain address (required)

Response:
```json
{
  "address": "proof1abc...",
  "balance": "100000000000000000000",
  "nonce": 5
}
```

#### Get Account Transactions

```
GET /account/{address}/transactions
```

Returns a list of transactions for the specified account address.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Parameters:
- `address`: The Proof Blockchain address (required)
- `page`: Page number for pagination (optional, default: 1)
- `limit`: Number of transactions per page (optional, default: 20, max: 100)

Response:
```json
{
  "transactions": [
    {
      "hash": "0xabc...",
      "from": "proof1abc...",
      "to": "proof1def...",
      "value": "1000000000000000000",
      "timestamp": 1620000000
    },
    ...
  ],
  "totalCount": 150,
  "page": 1,
  "limit": 20
}
```

### Transactions

#### Get Transaction Details

```
GET /transaction/{hash}
```

Returns details of a specific transaction.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Parameters:
- `hash`: The transaction hash (required)

Response:
```json
{
  "hash": "0xabc...",
  "from": "proof1abc...",
  "to": "proof1def...",
  "value": "1000000000000000000",
  "gasPrice": "20000000000",
  "gasLimit": "21000",
  "nonce": 5,
  "status": "confirmed",
  "blockNumber": 1234567,
  "timestamp": 1620000000
}
```

#### Send Transaction

```
POST /transaction/send
```

Submits a new transaction to the network.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Request Body:
```json
{
  "from": "proof1abc...",
  "to": "proof1def...",
  "value": "1000000000000000000",
  "gasPrice": "20000000000",
  "gasLimit": "21000",
  "nonce": 5,
  "data": "0x..." // Optional, for contract interactions
}
```

Response:
```json
{
  "hash": "0xabc...",
  "status": "pending"
}
```

### Blocks

#### Get Latest Block

```
GET /block/latest
```

Returns details of the latest block.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Response:
```json
{
  "number": 1234567,
  "hash": "0xabc...",
  "parentHash": "0xdef...",
  "timestamp": 1620000000,
  "transactions": ["0xghi...", "0xjkl..."],
  "size": 1234
}
```

#### Get Block by Number

```
GET /block/{number}
```

Returns details of a specific block.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Parameters:
- `number`: The block number (required)

Response: Same as Get Latest Block

### Smart Contracts

#### Call Smart Contract Function

```
POST /contract/{address}/call
```

Calls a read-only function on a smart contract.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Parameters:
- `address`: The contract address (required)

Request Body:
```json
{
  "function": "balanceOf",
  "params": ["proof1abc..."]
}
```

Response:
```json
{
  "result": "1000000000000000000"
}
```

### Network Statistics

#### Get Network Stats

```
GET /stats
```

Returns current network statistics.

Headers:
- `Authorization: Bearer your_jwt_token_here`
- `X-Proof-Key: your_proof_key_here`

Response:
```json
{
  "totalTransactions": 1234567890,
  "tps": 1000,
  "activeValidators": 101,
  "currentEpoch": 1234
}
```

## 6. Error Handling

All errors return JSON with the following structure:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "A human-readable error message"
  }
}
```

Common error codes:
- `UNAUTHORIZED`: Authentication failed
- `INVALID_PROOF_KEY`: Invalid or missing Proof Key
- `RATE_LIMIT_EXCEEDED`: Too many requests
- `INVALID_PARAMS`: Invalid parameters in the request
- `NOT_FOUND`: Requested resource not found
- `INTERNAL_ERROR`: Internal server error

## 7. Websocket API

For real-time updates, use our Websocket API:

```
wss://ws.api.proof.blockchain/v1
```

To connect, you need to provide your JWT token and Proof Key:

```javascript
const socket = new WebSocket('wss://ws.api.proof.blockchain/v1');

socket.onopen = function(e) {
  socket.send(JSON.stringify({
    type: 'auth',
    jwt: 'your_jwt_token_here',
    proofKey: 'your_proof_key_here'
  }));
};
```

Available subscriptions:
- `newBlocks`: Receive new block headers
- `pendingTransactions`: Receive pending transaction hashes

Example subscription:
```javascript
{
  "type": "subscribe",
  "channel": "newBlocks"
}
```

## 8. Security Best Practices

1. Never share your API key, JWT, or Proof Key
2. Use HTTPS for all API calls
3. Implement proper error handling
4. Regularly rotate your API keys
5. Use the principle of least privilege when requesting API access
6. Be aware that all data access attempts are logged on-chain using your Proof Key

## 9. Changelog

- 2024-10-01: v1.0.0 - Initial API release
- 2024-11-15: v1.1.0 - Added Websocket API
- 2024-12-01: v2.0.0 - Added Proof Key requirement for all requests

For support or questions, please contact api@proof.blockchain or visit our developer forum at https://forum.proof.blockchain/dev