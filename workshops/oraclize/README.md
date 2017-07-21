
# Getting Started with Oraclize
The following document will help you integrate Oraclize in your project. 

## Our Oracle Model
Oraclize works in an asynchronous way: 

* First, users will sent a transaction to a function in your smart contract. This function should contain an `oraclize_query`.
* Oraclize keeps monitoring the blockchain; when it will see an `oraclize_query` being called, it will fetch the data or compute an answer. 
* Oraclize will return the data to your smart-contract by sending a transaction to the `__callback` function, which you should include in your code.

The entire interaction should take around 30 seconds, mostly due to block confirmation times. 

`oraclize_query` is a function which accepts two mandatory arguments:

* *data sources*: one of the following value "URL","WolframAlpha", "IPFS", "computation", "nested", "random" 
* *query*: what you can pass as a query depends from the datasource. Eg. URL will expect an URL, while Wolfram Alpha an equation or a natural language expression 

More informations on datasources and what you can use them for it's available here:
http://docs.oraclize.it/#data-sources


## Integrating Oraclize in your Smart Contract

To integrate Oraclize in your smart-contract, you can use our Ethereum API which are available here:
https://github.com/oraclize/ethereum-api/blob/master/oraclizeAPI_0.4.sol

If you are using Remix/Browser-solidity, you can use the import statement and import them directly from Github, as in the example below.

```javascript
pragma solidity ^0.4.11;
import "github.com/oraclize/ethereum-api/oraclizeAPI.sol";

contract ExampleContract is usingOraclize {

    string public EURGBP;
    event updatedPrice(string price);

    function ExampleContract() payable {
        updatePrice();
    }

    function __callback(bytes32 myid, string result) {
        if (msg.sender != oraclize_cbAddress()) throw;
        EURGBP = result;
        updatedPrice(result);
    }

    function updatePrice() payable {
        oraclize_query("URL", "json(http://api.fixer.io/latest?symbols=USD,GBP).rates.GBP");
    }
}

```

As you can see, the first thing to do is to make your contract inherit the methods of the usingOraclize contract present in the oraclizeAPI.sol. This usingOraclize contract contains all the methods and helpers to interface with Oraclize correctly.

The ExampleContract above is simple: when the function updatePrice is executed, `oraclize_query` is called. In this case with the data-source URL and a query. The query in this case is constituted by an URL with a JSON parser applied.

The result, which is the current EUR/GBP exchange rate, is returned as the result argument (as a string) in the callback function, which you see defined in the example.

**Note**: Oraclize works on a pay-per-call fee model. In order for Oraclize to work, the contract should have a balance or alternatively value must be send with the transaction executing `oraclize_query`. The fee is taken automatically and correctly by the oraclize_query.

## Testing the Code
You can test your contracts in a private testnet or on the public Ethereum testnet: Kovan, Rinkeby and Ropsten.
If you want to test your smart contracts in your own private testnet, you can still integrate with Oraclize by using the ethereum-bridge: https://github.com/oraclize/ethereum-bridge

## More Examples
You can find more examples at this page:
https://github.com/oraclize/ethereum-examples/tree/master/solidity

## Development Resources
Oraclize IDE (forked from browser-solidity/Remix)
http://dapps.oraclize.it/browser-solidity/#gist=9817193e5b05206847ed1fcd1d16bd1d&version=soljson-v0.4.13+commit.fb4cb1a.js

This fork of browser-solidity makes early prototyping easy, as contract are deployed in the browser-memory and they interact quickly with Oraclize without having to wait for block times. You will see the query to Oraclize and the answer in the Oraclize tab. 

## More Information
A much more complete documentation is available at:
- https://docs.oraclize.it
