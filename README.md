# mevETH Protocol Data Resources

## mevETH Events

> 23 events found in contract MevEth:

1.  AdminAdded
2.  AdminDeleted
3.  Approval
4.  CreamRedeemed
5.  Deposit
6.  MevEthInitialized
7.  MevEthShareVaultUpdateCanceled
8.  MevEthShareVaultUpdateCommitted
9.  MevEthShareVaultUpdateFinalized
10.  OperatorAdded
11.  OperatorDeleted
12.  Rewards
13.  StakingModuleUpdateCanceled
14.  StakingModuleUpdateCommitted
15.  StakingModuleUpdateFinalized
16.  StakingPaused
17.  StakingUnpaused
18.  Transfer
19.  ValidatorCreated
20.  ValidatorWithdraw
21.  Withdraw
22.  WithdrawalQueueClosed
23.  WithdrawalQueueOpened

70 functions found in contract MevEth:

1.  CREAM\_TO\_MEV\_ETH\_PERCENT
2.  DOMAIN\_SEPARATOR
3.  MIN\_DEPOSIT
4.  MIN\_WITHDRAWAL
5.  WETH9
6.  addAdmin
7.  addOperator
8.  admins
9.  allowance
10.  approve
11.  asset
12.  balanceOf
13.  calculateNeededEtherBuffer
14.  cancelUpdateMevEthShareVault
15.  cancelUpdateStakingModule
16.  claim
17.  commitUpdateMevEthShareVault
18.  commitUpdateStakingModule
19.  convertToAssets
20.  convertToShares
21.  creamToken
22.  createValidator
23.  decimals
24.  deleteAdmin
25.  deleteOperator
26.  deposit
27.  finalizeUpdateMevEthShareVault
28.  finalizeUpdateStakingModule
29.  fraction
30.  grantRewards
31.  grantValidatorWithdraw
32.  init
33.  initialized
34.  maxDeposit
35.  maxMint
36.  maxRedeem
37.  maxWithdraw
38.  mevEthShareVault
39.  mint
40.  name
41.  nonces
42.  operators
43.  pauseStaking
44.  pendingMevEthShareVault
45.  pendingMevEthShareVaultCommittedTimestamp
46.  pendingStakingModule
47.  pendingStakingModuleCommittedTimestamp
48.  permit
49.  previewDeposit
50.  previewMint
51.  previewRedeem
52.  previewWithdraw
53.  processWithdrawalQueue
54.  queueLength
55.  redeem
56.  redeemCream
57.  requestsFinalisedUntil
58.  setMinWithdrawal
59.  stakingModule
60.  stakingPaused
61.  symbol
62.  totalAssets
63.  totalSupply
64.  transfer
65.  transferFrom
66.  unpauseStaking
67.  withdraw
68.  withdrawQueue
69.  withdrawalAmountQueued
70.  withdrawalQueue

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`newAdmin` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "newAdmin", "type": "address"}], "name": "AdminAdded", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x44d6d25963f097ad14f29f06854a01f575648a1ef82f30e562ccd3889717e339'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.newAdmin AS `newAdmin`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22AdminAdded%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_AdminAdded%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldAdmin` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldAdmin", "type": "address"}], "name": "AdminDeleted", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x989ddfce057dad219e0ae16f691b121bb0e348f0d8ae0ad400b4d5ac8d616c8b'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldAdmin AS `oldAdmin`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22AdminDeleted%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_AdminDeleted%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`owner` STRING, `spender` STRING, `amount` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "owner", "type": "address"}, {"indexed": true, "internalType": "address", "name": "spender", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "Approval", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.owner AS `owner`
    ,parsed.spender AS `spender`
    ,parsed.amount AS `amount`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22spender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22Approval%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22spender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_Approval%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "CREAM_TO_MEV_ETH_PERCENT", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x6ca6f0fe')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22CREAM_TO_MEV_ETH_PERCENT%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_CREAM_TO_MEV_ETH_PERCENT%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`redeemer` STRING, `creamAmount` STRING, `mevEthAmount` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "redeemer", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "creamAmount", "type": "uint256"}, {"indexed": false, "internalType": "uint256", "name": "mevEthAmount", "type": "uint256"}], "name": "CreamRedeemed", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x08a1751668afae790ff5a3e76783eb5dc7c53adc0b248d4af119bf0edb29f97c'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.redeemer AS `redeemer`
    ,parsed.creamAmount AS `creamAmount`
    ,parsed.mevEthAmount AS `mevEthAmount`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22redeemer%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22creamAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22mevEthAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22CreamRedeemed%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22redeemer%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22creamAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22mevEthAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_CreamRedeemed%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "DOMAIN_SEPARATOR", "outputs": [{"internalType": "bytes32", "name": "", "type": "bytes32"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x3644e515')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22DOMAIN_SEPARATOR%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_DOMAIN_SEPARATOR%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`caller` STRING, `owner` STRING, `assets` STRING, `shares` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "caller", "type": "address"}, {"indexed": true, "internalType": "address", "name": "owner", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "assets", "type": "uint256"}, {"indexed": false, "internalType": "uint256", "name": "shares", "type": "uint256"}], "name": "Deposit", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xdcbc1c05240f31ff3ad067ef1ee35ce4997762752e3a095284754544f4c709d7'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.caller AS `caller`
    ,parsed.owner AS `owner`
    ,parsed.assets AS `assets`
    ,parsed.shares AS `shares`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22caller%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22Deposit%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22caller%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_Deposit%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "MIN_DEPOSIT", "outputs": [{"internalType": "uint128", "name": "", "type": "uint128"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xe1e158a5')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22MIN_DEPOSIT%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_MIN_DEPOSIT%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "MIN_WITHDRAWAL", "outputs": [{"internalType": "uint128", "name": "", "type": "uint128"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xd15ca166')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22MIN_WITHDRAWAL%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_MIN_WITHDRAWAL%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`mevEthShareVault` STRING, `stakingModule` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "mevEthShareVault", "type": "address"}, {"indexed": true, "internalType": "address", "name": "stakingModule", "type": "address"}], "name": "MevEthInitialized", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x64ba02ab01156808d0b519bed16cc382b3fc7fbe9bae6951b30fb08742b824a8'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.mevEthShareVault AS `mevEthShareVault`
    ,parsed.stakingModule AS `stakingModule`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22mevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22stakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22MevEthInitialized%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22mevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22stakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_MevEthInitialized%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldVault` STRING, `newVault` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldVault", "type": "address"}, {"indexed": true, "internalType": "address", "name": "newVault", "type": "address"}], "name": "MevEthShareVaultUpdateCanceled", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x84251438ec5abdb3e7f88a1f74e49cc798585f96428d53f9b3b85232b7f4bde3'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldVault AS `oldVault`
    ,parsed.newVault AS `newVault`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22MevEthShareVaultUpdateCanceled%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_MevEthShareVaultUpdateCanceled%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldVault` STRING, `pendingVault` STRING, `eligibleForFinalization` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldVault", "type": "address"}, {"indexed": true, "internalType": "address", "name": "pendingVault", "type": "address"}, {"indexed": true, "internalType": "uint64", "name": "eligibleForFinalization", "type": "uint64"}], "name": "MevEthShareVaultUpdateCommitted", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xa8aa7c0b023219361c11e0a52a6ae2e6b7404aa61f5df0fc03d6cb8acafd66bf'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldVault AS `oldVault`
    ,parsed.pendingVault AS `pendingVault`
    ,parsed.eligibleForFinalization AS `eligibleForFinalization`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint64%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22eligibleForFinalization%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint64%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22MevEthShareVaultUpdateCommitted%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22eligibleForFinalization%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_MevEthShareVaultUpdateCommitted%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldVault` STRING, `newVault` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldVault", "type": "address"}, {"indexed": true, "internalType": "address", "name": "newVault", "type": "address"}], "name": "MevEthShareVaultUpdateFinalized", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x4dfa26cce610e1567cfad6de12824202e3394a8e66665914b3aeec46b60eca11'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldVault AS `oldVault`
    ,parsed.newVault AS `newVault`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22MevEthShareVaultUpdateFinalized%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_MevEthShareVaultUpdateFinalized%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`newOperator` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "newOperator", "type": "address"}], "name": "OperatorAdded", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xac6fa858e9350a46cec16539926e0fde25b7629f84b5a72bffaae4df888ae86d'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.newOperator AS `newOperator`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22OperatorAdded%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_OperatorAdded%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldOperator` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldOperator", "type": "address"}], "name": "OperatorDeleted", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x69df2c5ec2ea4d1fbe1e503524f593b356162ca710671263827f2e1992b95ae1'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldOperator AS `oldOperator`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22OperatorDeleted%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_OperatorDeleted%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`sender` STRING, `amount` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": false, "internalType": "address", "name": "sender", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "Rewards", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xc083a1647e3ee591bf42b82564ffb4d16fdbb26068f0080da911c8d8300fd84a'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.sender AS `sender`
    ,parsed.amount AS `amount`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22sender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22Rewards%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22sender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_Rewards%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldModule` STRING, `pendingModule` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldModule", "type": "address"}, {"indexed": true, "internalType": "address", "name": "pendingModule", "type": "address"}], "name": "StakingModuleUpdateCanceled", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x372791c0ff91275afe8e3b839b282b0dbb7bb639dbe7cd5896eedfec4c8ed8c6'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldModule AS `oldModule`
    ,parsed.pendingModule AS `pendingModule`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22StakingModuleUpdateCanceled%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_StakingModuleUpdateCanceled%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldModule` STRING, `pendingModule` STRING, `eligibleForFinalization` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldModule", "type": "address"}, {"indexed": true, "internalType": "address", "name": "pendingModule", "type": "address"}, {"indexed": true, "internalType": "uint64", "name": "eligibleForFinalization", "type": "uint64"}], "name": "StakingModuleUpdateCommitted", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x39610571f23fd1a159473075de5b697023e7a31da8488147ecce3c05489885fa'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldModule AS `oldModule`
    ,parsed.pendingModule AS `pendingModule`
    ,parsed.eligibleForFinalization AS `eligibleForFinalization`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint64%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22eligibleForFinalization%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint64%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22StakingModuleUpdateCommitted%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22eligibleForFinalization%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_StakingModuleUpdateCommitted%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`oldModule` STRING, `newModule` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "oldModule", "type": "address"}, {"indexed": true, "internalType": "address", "name": "newModule", "type": "address"}], "name": "StakingModuleUpdateFinalized", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x2d2c1ec12191e7f1a0c23a865475c7abecc7f26edb6c409defa31748b28a5013'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.oldModule AS `oldModule`
    ,parsed.newModule AS `newModule`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22StakingModuleUpdateFinalized%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_StakingModuleUpdateFinalized%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [], "name": "StakingPaused", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x26d1807b479eaba249c1214b82e4b65bbb0cc73ee8a17901324b1ef1b5904e49'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22StakingPaused%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_StakingPaused%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [], "name": "StakingUnpaused", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xa75958c26fdcd449db08b7c754dcddd7a15b023665ee9dbd2ef62d8e1befaa4a'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22StakingUnpaused%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_StakingUnpaused%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`from` STRING, `to` STRING, `amount` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "from", "type": "address"}, {"indexed": true, "internalType": "address", "name": "to", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "Transfer", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.from AS `from`
    ,parsed.to AS `to`
    ,parsed.amount AS `amount`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22from%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22to%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22Transfer%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22from%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22to%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_Transfer%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`stakingModule` STRING, `newValidator` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "stakingModule", "type": "address"}, {"components": [{"internalType": "address", "name": "operator", "type": "address"}, {"internalType": "bytes", "name": "pubkey", "type": "bytes"}, {"internalType": "bytes32", "name": "withdrawal_credentials", "type": "bytes32"}, {"internalType": "bytes", "name": "signature", "type": "bytes"}, {"internalType": "bytes32", "name": "deposit_data_root", "type": "bytes32"}], "indexed": false, "internalType": "struct IStakingModule.ValidatorData", "name": "newValidator", "type": "tuple"}], "name": "ValidatorCreated", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x8a8ef37c52979cf8197dd24ed66c48fbd26d1b35ee1879d8c0c6be67b64fe756'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.stakingModule AS `stakingModule`
    ,parsed.newValidator AS `newValidator`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22stakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22components%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22operator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pubkey%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawal_credentials%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22signature%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deposit_data_root%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22struct%20IStakingModule.ValidatorData%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newValidator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22tuple%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22ValidatorCreated%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22stakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22fields%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22operator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pubkey%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawal_credentials%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22signature%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deposit_data_root%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newValidator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22RECORD%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_ValidatorCreated%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`sender` STRING, `amount` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": false, "internalType": "address", "name": "sender", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "ValidatorWithdraw", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x12b964a3993d1598dd8a3b627a3b90b4bc6b7a8f4f8bb6afde02a30d178e28ef'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.sender AS `sender`
    ,parsed.amount AS `amount`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22sender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22ValidatorWithdraw%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22sender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_ValidatorWithdraw%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "WETH9", "outputs": [{"internalType": "contract WETH", "name": "", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x4aa4a4fc')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22WETH9%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22contract%20WETH%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_WETH9%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`caller` STRING, `receiver` STRING, `owner` STRING, `assets` STRING, `shares` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "caller", "type": "address"}, {"indexed": true, "internalType": "address", "name": "receiver", "type": "address"}, {"indexed": true, "internalType": "address", "name": "owner", "type": "address"}, {"indexed": false, "internalType": "uint256", "name": "assets", "type": "uint256"}, {"indexed": false, "internalType": "uint256", "name": "shares", "type": "uint256"}], "name": "Withdraw", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0xfbde797d201c681b91056529119e0b02407c7bb96a4a2c75c01fc9667232c8db'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.caller AS `caller`
    ,parsed.receiver AS `receiver`
    ,parsed.owner AS `owner`
    ,parsed.assets AS `assets`
    ,parsed.shares AS `shares`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22caller%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22Withdraw%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22caller%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_Withdraw%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`recipient` STRING, `withdrawalId` STRING, `assets` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "recipient", "type": "address"}, {"indexed": true, "internalType": "uint256", "name": "withdrawalId", "type": "uint256"}, {"indexed": false, "internalType": "uint256", "name": "assets", "type": "uint256"}], "name": "WithdrawalQueueClosed", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x54a5cca61d01babb886db109822515b9fdff5360b38a042acfb13e47fab8b6fe'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.recipient AS `recipient`
    ,parsed.withdrawalId AS `withdrawalId`
    ,parsed.assets AS `assets`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22recipient%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalId%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22WithdrawalQueueClosed%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22recipient%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalId%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_WithdrawalQueueClosed%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
  PARSE_LOG(data STRING, topics ARRAY<STRING>)
  RETURNS STRUCT<`recipient` STRING, `withdrawalId` STRING, `assets` STRING>
  LANGUAGE js AS """
    var parsedEvent = {"anonymous": false, "inputs": [{"indexed": true, "internalType": "address", "name": "recipient", "type": "address"}, {"indexed": true, "internalType": "uint256", "name": "withdrawalId", "type": "uint256"}, {"indexed": false, "internalType": "uint256", "name": "assets", "type": "uint256"}], "name": "WithdrawalQueueOpened", "type": "event"}
    return abi.decodeEvent(parsedEvent, data, topics, false);
"""
OPTIONS
  ( library="https://storage.googleapis.com/ethlab-183014.appspot.com/ethjs-abi.js" );

WITH parsed_logs AS
(SELECT
    logs.block_timestamp AS block_timestamp
    ,logs.block_number AS block_number
    ,logs.transaction_hash AS transaction_hash
    ,logs.log_index AS log_index
    ,PARSE_LOG(logs.data, logs.topics) AS parsed
FROM `bigquery-public-data.crypto_ethereum.logs` AS logs
WHERE address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND topics[SAFE_OFFSET(0)] = '0x09dfd37369506d687db24de2b5f681eb0050ccd07eaafa95d0252899471dd740'
)
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,log_index
    ,parsed.recipient AS `recipient`
    ,parsed.withdrawalId AS `withdrawalId`
    ,parsed.assets AS `assets`
FROM parsed_logs
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22anonymous%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22recipient%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20true%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalId%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22indexed%22%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22WithdrawalQueueOpened%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22event%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22log%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22recipient%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalId%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_WithdrawalQueueOpened%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newAdmin` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "newAdmin", "type": "address"}], "name": "addAdmin", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x70480275')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newAdmin AS `newAdmin`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22addAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_addAdmin%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newOperator` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "newOperator", "type": "address"}], "name": "addOperator", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x9870d7fe')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newOperator AS `newOperator`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22addOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_addOperator%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}], "name": "admins", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x429b62e5')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22admins%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_admins%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, `` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}, {"internalType": "address", "name": "", "type": "address"}], "name": "allowance", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xdd62ed3e')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22allowance%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_allowance%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`spender` STRING, `amount` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "spender", "type": "address"}, {"internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "approve", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x095ea7b3')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.spender AS `spender`
    
    ,parsed.amount AS `amount`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22spender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22approve%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22spender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_approve%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "asset", "outputs": [{"internalType": "address", "name": "assetTokenAddress", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x38d52e0f')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22asset%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assetTokenAddress%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_asset%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}], "name": "balanceOf", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x70a08231')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22balanceOf%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_balanceOf%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "calculateNeededEtherBuffer", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x82b9ebaa')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22calculateNeededEtherBuffer%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_calculateNeededEtherBuffer%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "cancelUpdateMevEthShareVault", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xddc2f1ab')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22cancelUpdateMevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_cancelUpdateMevEthShareVault%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "cancelUpdateStakingModule", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xbbbad849')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22cancelUpdateStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_cancelUpdateStakingModule%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`withdrawalId` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "withdrawalId", "type": "uint256"}], "name": "claim", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x379607f5')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.withdrawalId AS `withdrawalId`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalId%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22claim%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalId%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_claim%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newMevEthShareVault` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "newMevEthShareVault", "type": "address"}], "name": "commitUpdateMevEthShareVault", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xaa1cb376')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newMevEthShareVault AS `newMevEthShareVault`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newMevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22commitUpdateMevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newMevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_commitUpdateMevEthShareVault%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newModule` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "contract IStakingModule", "name": "newModule", "type": "address"}], "name": "commitUpdateStakingModule", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x95849aa4')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newModule AS `newModule`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22contract%20IStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22commitUpdateStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_commitUpdateStakingModule%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`shares` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "name": "convertToAssets", "outputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x07a2d13a')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.shares AS `shares`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22convertToAssets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_convertToAssets%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`assets` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "name": "convertToShares", "outputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xc6e6f592')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.assets AS `assets`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22convertToShares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_convertToShares%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "creamToken", "outputs": [{"internalType": "address", "name": "", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xdf2d43d8')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22creamToken%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_creamToken%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newData` STRING, `latestDepositRoot` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"components": [{"internalType": "address", "name": "operator", "type": "address"}, {"internalType": "bytes", "name": "pubkey", "type": "bytes"}, {"internalType": "bytes32", "name": "withdrawal_credentials", "type": "bytes32"}, {"internalType": "bytes", "name": "signature", "type": "bytes"}, {"internalType": "bytes32", "name": "deposit_data_root", "type": "bytes32"}], "internalType": "struct IStakingModule.ValidatorData", "name": "newData", "type": "tuple"}, {"internalType": "bytes32", "name": "latestDepositRoot", "type": "bytes32"}], "name": "createValidator", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x8a1c2426')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newData AS `newData`
    
    ,parsed.latestDepositRoot AS `latestDepositRoot`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22components%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22operator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pubkey%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawal_credentials%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22signature%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deposit_data_root%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22struct%20IStakingModule.ValidatorData%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newData%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22tuple%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22latestDepositRoot%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22createValidator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22fields%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22operator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pubkey%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawal_credentials%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22signature%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deposit_data_root%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newData%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22RECORD%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22latestDepositRoot%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_createValidator%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "decimals", "outputs": [{"internalType": "uint8", "name": "", "type": "uint8"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x313ce567')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22decimals%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint8%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint8%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_decimals%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`oldAdmin` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "oldAdmin", "type": "address"}], "name": "deleteAdmin", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x27e1f7df')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.oldAdmin AS `oldAdmin`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deleteAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldAdmin%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_deleteAdmin%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`oldOperator` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "oldOperator", "type": "address"}], "name": "deleteOperator", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xb40992a1')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.oldOperator AS `oldOperator`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deleteOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22oldOperator%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_deleteOperator%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`assets` STRING, `receiver` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}, {"internalType": "address", "name": "receiver", "type": "address"}], "name": "deposit", "outputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "stateMutability": "payable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x6e553f65')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.assets AS `assets`
    
    ,parsed.receiver AS `receiver`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deposit%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22payable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_deposit%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "finalizeUpdateMevEthShareVault", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xbc74efe8')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22finalizeUpdateMevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_finalizeUpdateMevEthShareVault%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "finalizeUpdateStakingModule", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x9ed89c91')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22finalizeUpdateStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_finalizeUpdateStakingModule%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "fraction", "outputs": [{"internalType": "uint128", "name": "elastic", "type": "uint128"}, {"internalType": "uint128", "name": "base", "type": "uint128"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xd8894bb5')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22fraction%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22elastic%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22base%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_fraction%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "grantRewards", "outputs": [], "stateMutability": "payable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x558cb7f7')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22grantRewards%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22payable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_grantRewards%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "grantValidatorWithdraw", "outputs": [], "stateMutability": "payable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xfe183211')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22grantValidatorWithdraw%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22payable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_grantValidatorWithdraw%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`initialShareVault` STRING, `initialStakingModule` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "initialShareVault", "type": "address"}, {"internalType": "address", "name": "initialStakingModule", "type": "address"}], "name": "init", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xf09a4016')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.initialShareVault AS `initialShareVault`
    
    ,parsed.initialStakingModule AS `initialStakingModule`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22initialShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22initialStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22init%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22initialShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22initialStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_init%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "initialized", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x158ef93e')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22initialized%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_initialized%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}], "name": "maxDeposit", "outputs": [{"internalType": "uint256", "name": "maxAssets", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x402d267d')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxDeposit%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxAssets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_maxDeposit%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}], "name": "maxMint", "outputs": [{"internalType": "uint256", "name": "maxShares", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xc63d75b6')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxMint%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxShares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_maxMint%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`owner` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "owner", "type": "address"}], "name": "maxRedeem", "outputs": [{"internalType": "uint256", "name": "maxShares", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xd905777e')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.owner AS `owner`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxRedeem%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxShares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_maxRedeem%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`owner` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "owner", "type": "address"}], "name": "maxWithdraw", "outputs": [{"internalType": "uint256", "name": "maxAssets", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xce96cb77')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.owner AS `owner`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxWithdraw%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22maxAssets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_maxWithdraw%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "mevEthShareVault", "outputs": [{"internalType": "address", "name": "", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xf9cc45f2')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22mevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_mevEthShareVault%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`shares` STRING, `receiver` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}, {"internalType": "address", "name": "receiver", "type": "address"}], "name": "mint", "outputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "stateMutability": "payable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x94bf804d')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.shares AS `shares`
    
    ,parsed.receiver AS `receiver`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22mint%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22payable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_mint%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "name", "outputs": [{"internalType": "string", "name": "", "type": "string"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x06fdde03')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22name%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22string%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22string%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_name%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}], "name": "nonces", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x7ecebe00')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22nonces%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_nonces%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "", "type": "address"}], "name": "operators", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x13e7c9d8')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed. AS ``
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22operators%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_operators%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "pauseStaking", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xf999c506')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pauseStaking%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_pauseStaking%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "pendingMevEthShareVault", "outputs": [{"internalType": "address", "name": "", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xd02aaa65')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingMevEthShareVault%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_pendingMevEthShareVault%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "pendingMevEthShareVaultCommittedTimestamp", "outputs": [{"internalType": "uint64", "name": "", "type": "uint64"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x6a4c6618')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingMevEthShareVaultCommittedTimestamp%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint64%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint64%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_pendingMevEthShareVaultCommittedTimestamp%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "pendingStakingModule", "outputs": [{"internalType": "contract IStakingModule", "name": "", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x72cf7751')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22contract%20IStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_pendingStakingModule%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "pendingStakingModuleCommittedTimestamp", "outputs": [{"internalType": "uint64", "name": "", "type": "uint64"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x3cb5c588')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22pendingStakingModuleCommittedTimestamp%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint64%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint64%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_pendingStakingModuleCommittedTimestamp%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`owner` STRING, `spender` STRING, `value` STRING, `deadline` STRING, `v` STRING, `r` STRING, `s` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "owner", "type": "address"}, {"internalType": "address", "name": "spender", "type": "address"}, {"internalType": "uint256", "name": "value", "type": "uint256"}, {"internalType": "uint256", "name": "deadline", "type": "uint256"}, {"internalType": "uint8", "name": "v", "type": "uint8"}, {"internalType": "bytes32", "name": "r", "type": "bytes32"}, {"internalType": "bytes32", "name": "s", "type": "bytes32"}], "name": "permit", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xd505accf')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.owner AS `owner`
    
    ,parsed.spender AS `spender`
    
    ,parsed.value AS `value`
    
    ,parsed.deadline AS `deadline`
    
    ,parsed.v AS `v`
    
    ,parsed.r AS `r`
    
    ,parsed.s AS `s`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22spender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22value%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deadline%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint8%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22v%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint8%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22r%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bytes32%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22s%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bytes32%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22permit%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22spender%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22value%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22deadline%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22v%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22r%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22s%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_permit%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`assets` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "name": "previewDeposit", "outputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xef8b30f7')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.assets AS `assets`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22previewDeposit%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_previewDeposit%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`shares` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "name": "previewMint", "outputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xb3d7f6b9')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.shares AS `shares`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22previewMint%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_previewMint%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`shares` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "name": "previewRedeem", "outputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x4cdad506')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.shares AS `shares`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22previewRedeem%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_previewRedeem%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`assets` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "name": "previewWithdraw", "outputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x0a28a477')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.assets AS `assets`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22previewWithdraw%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_previewWithdraw%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newRequestsFinalisedUntil` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "newRequestsFinalisedUntil", "type": "uint256"}], "name": "processWithdrawalQueue", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x342c00b3')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newRequestsFinalisedUntil AS `newRequestsFinalisedUntil`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newRequestsFinalisedUntil%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22processWithdrawalQueue%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newRequestsFinalisedUntil%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_processWithdrawalQueue%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "queueLength", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xab91c7b0')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22queueLength%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_queueLength%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`shares` STRING, `receiver` STRING, `owner` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}, {"internalType": "address", "name": "receiver", "type": "address"}, {"internalType": "address", "name": "owner", "type": "address"}], "name": "redeem", "outputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xba087652')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.shares AS `shares`
    
    ,parsed.receiver AS `receiver`
    
    ,parsed.owner AS `owner`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22redeem%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_redeem%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`creamAmount` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "creamAmount", "type": "uint256"}], "name": "redeemCream", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xc1a7a813')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.creamAmount AS `creamAmount`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22creamAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22redeemCream%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22creamAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_redeemCream%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "requestsFinalisedUntil", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xeb09200a')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22requestsFinalisedUntil%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_requestsFinalisedUntil%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`newMinimum` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint128", "name": "newMinimum", "type": "uint128"}], "name": "setMinWithdrawal", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x8865cf50')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.newMinimum AS `newMinimum`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newMinimum%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22setMinWithdrawal%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22newMinimum%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_setMinWithdrawal%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "stakingModule", "outputs": [{"internalType": "contract IStakingModule", "name": "", "type": "address"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x504b82bf')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22stakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22contract%20IStakingModule%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_stakingModule%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "stakingPaused", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xbbb781cc')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22stakingPaused%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_stakingPaused%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "symbol", "outputs": [{"internalType": "string", "name": "", "type": "string"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x95d89b41')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22symbol%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22string%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22string%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_symbol%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "totalAssets", "outputs": [{"internalType": "uint256", "name": "totalManagedAssets", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x01e1d114')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22totalAssets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22totalManagedAssets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_totalAssets%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "totalSupply", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x18160ddd')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22totalSupply%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_totalSupply%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`to` STRING, `amount` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "to", "type": "address"}, {"internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "transfer", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xa9059cbb')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.to AS `to`
    
    ,parsed.amount AS `amount`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22to%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22transfer%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22to%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_transfer%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`from` STRING, `to` STRING, `amount` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "address", "name": "from", "type": "address"}, {"internalType": "address", "name": "to", "type": "address"}, {"internalType": "uint256", "name": "amount", "type": "uint256"}], "name": "transferFrom", "outputs": [{"internalType": "bool", "name": "", "type": "bool"}], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x23b872dd')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.from AS `from`
    
    ,parsed.to AS `to`
    
    ,parsed.amount AS `amount`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22from%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22to%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22transferFrom%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22from%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22to%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_transferFrom%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "unpauseStaking", "outputs": [], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x93f4bcde')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22unpauseStaking%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_unpauseStaking%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`assets` STRING, `receiver` STRING, `owner` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}, {"internalType": "address", "name": "receiver", "type": "address"}, {"internalType": "address", "name": "owner", "type": "address"}], "name": "withdraw", "outputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xb460af94')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.assets AS `assets`
    
    ,parsed.receiver AS `receiver`
    
    ,parsed.owner AS `owner`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdraw%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_withdraw%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`assets` STRING, `receiver` STRING, `owner` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "assets", "type": "uint256"}, {"internalType": "address", "name": "receiver", "type": "address"}, {"internalType": "address", "name": "owner", "type": "address"}], "name": "withdrawQueue", "outputs": [{"internalType": "uint256", "name": "shares", "type": "uint256"}], "stateMutability": "nonpayable", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xbeb8db56')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.assets AS `assets`
    
    ,parsed.receiver AS `receiver`
    
    ,parsed.owner AS `owner`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawQueue%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22shares%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22nonpayable%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22assets%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22owner%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_withdrawQueue%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [], "name": "withdrawalAmountQueued", "outputs": [{"internalType": "uint256", "name": "", "type": "uint256"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0x2e92056d')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalAmountQueued%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_withdrawalAmountQueued%22%0A%20%20%20%20%7D%0A%7D)

```

CREATE TEMP FUNCTION
    PARSE_TRACE(data STRING)
    RETURNS STRUCT<`ticketNumber` STRING, error STRING>
    LANGUAGE js AS """
    var abi = {"inputs": [{"internalType": "uint256", "name": "ticketNumber", "type": "uint256"}], "name": "withdrawalQueue", "outputs": [{"internalType": "bool", "name": "claimed", "type": "bool"}, {"internalType": "address", "name": "receiver", "type": "address"}, {"internalType": "uint128", "name": "amount", "type": "uint128"}, {"internalType": "uint128", "name": "accumulatedAmount", "type": "uint128"}], "stateMutability": "view", "type": "function"};
    var interface_instance = new ethers.utils.Interface([abi]);

    var result = {};
    try {
        var parsedTransaction = interface_instance.parseTransaction({data: data});
        var parsedArgs = parsedTransaction.args;

        if (parsedArgs && parsedArgs.length >= abi.inputs.length) {
            for (var i = 0; i < abi.inputs.length; i++) {
                var paramName = abi.inputs[i].name;
                var paramValue = parsedArgs[i];
                if (abi.inputs[i].type === 'address' && typeof paramValue === 'string') {
                    // For consistency all addresses are lowercase.
                    paramValue = paramValue.toLowerCase();
                }
                result[paramName] = paramValue;
            }
        } else {
            result['error'] = 'Parsed transaction args is empty or has too few values.';
        }
    } catch (e) {
        result['error'] = e.message;
    }

    return result;
"""
OPTIONS
  ( library="gs://blockchain-etl-bigquery/ethers.js" );

WITH parsed_traces AS
(SELECT
    traces.block_timestamp AS block_timestamp
    ,traces.block_number AS block_number
    ,traces.transaction_hash AS transaction_hash
    ,traces.trace_address AS trace_address
    ,PARSE_TRACE(traces.input) AS parsed
FROM `bigquery-public-data.crypto_ethereum.traces` AS traces
WHERE to_address = '0x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e'
  AND STARTS_WITH(traces.input, '0xc822adda')
  )
SELECT
     block_timestamp
     ,block_number
     ,transaction_hash
     ,trace_address
     ,parsed.error AS error
     
    ,parsed.ticketNumber AS `ticketNumber`
    
FROM parsed_traces
```

[Download Table Definition](data: text/json;charset=utf-8,%7B%0A%20%20%20%20%22parser%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22abi%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%22inputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint256%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22ticketNumber%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint256%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22withdrawalQueue%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22outputs%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22bool%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22claimed%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22bool%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22address%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22receiver%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22address%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22amount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22internalType%22%3A%20%22uint128%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22accumulatedAmount%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22uint128%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22stateMutability%22%3A%20%22view%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22function%22%0A%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%22contract_address%22%3A%20%220x24ae2da0f361aa4be46b48eb19c91e02c5e4f27e%22%2C%0A%20%20%20%20%20%20%20%20%22field_mapping%22%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%22type%22%3A%20%22trace%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22table%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22dataset_name%22%3A%20%22%3CINSERT_DATASET_NAME%3E%22%2C%0A%20%20%20%20%20%20%20%20%22schema%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22name%22%3A%20%22ticketNumber%22%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%22type%22%3A%20%22STRING%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%5D%2C%0A%20%20%20%20%20%20%20%20%22table_description%22%3A%20%22%22%2C%0A%20%20%20%20%20%20%20%20%22table_name%22%3A%20%22%3CTABLE_PREFIX%3E_event_withdrawalQueue%22%0A%20%20%20%20%7D%0A%7D)
