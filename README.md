# piperSwap
Decentralized Exchange Application 

PiperSwap is a Decentralized Exchange Application where we have created a Platform which would accept Tokens from the User and in return will provide some PToken (Piper Token).

Technologies Used:
1. Blockchain: Ethereum
2. Smart Contract Language: Solidity
3. Limit Order Protocol: 1inch Limit Order Protocol
4. FrontEnd: JavaScript and Css
5. Frameworks: Web3, React.js and Moralis.


Working of the Application:
1. Connect your Metamask Wallet with the Application.
2. Enter the amount of Dai Token you need to invest.
3. You will recive some PiperToken in return of the Dai Token

Internal Working of the System:
1. The Dai Token recived from the user will be used to set Limit Orders using 1inch Limit-Order-Protocol
2. This Limit Order will be set Automatically at an interval.
3.  MakerAsset: '0x4F96Fe3b7A6Cf9725f59d353F723c1bDb64CA6Aa' (Dai)
    TakerAsset: '0xd0a1e359811322d97991e03f863a0c30c2cf029c' (WEth)

Commands to Run Project:
1. Clone the Repo
2. run npm install
3. React App: npm run start
4. Limit-order App: truffle --network kovan limit.js

Some Important Address:
Token Address: 
1. '0x4F96Fe3b7A6Cf9725f59d353F723c1bDb64CA6Aa' (Dai)
2. '0xd0a1e359811322d97991e03f863a0c30c2cf029c' (WEth)
3. Contract Address: '0x2BC7E7123CDFdA75722E1E745098FA8016731602'
4. 1inch Limit Order Address: '0x94Bc2a1C732BcAd7343B25af48385Fe76E08734f'

1inch Protocol Examples:

1. Build Limit Order: 
   
   const limitOrder = await limitOrderBuilder.buildLimitOrder({
        makerAssetAddress: '0x4F96Fe3b7A6Cf9725f59d353F723c1bDb64CA6Aa',
        takerAssetAddress: '0xd0a1e359811322d97991e03f863a0c30c2cf029c',
        makerAddress: walletAddress,
        makerAmount: '100',
        takerAmount: '0',
        predicate: simplePredicate,
       
        
    });
2. Limit Order Typed Data:
    
    const limitOrderTypedData = await limitOrderBuilder.buildLimitOrderTypedData(
        limitOrder
    );
3. Sign Limit Order:
    
    const limitOrderSignature = await privateKeyProviderConnector.signTypedData(
        walletAddress,
        limitOrderTypedData
    );

4. Fill Limit Order:
     
     const callData = await limitOrderProtocolFacade.fillLimitOrder(
        order,
        signature,
        makerAmount,
        takerAmount,
        thresholdAmount
    );

5. Send Limit Order:
    
    const res = await contract.methods.fillOrder(order,
            signature,
            makerAmount,
            takerAmount,
            thresholdAmount).send({
            from: walletAddress,
            // gas: 2100000, // Set your gas limit
            // gasPrice: 40000, // Set your gas price
            to: contractAddress,
            data: callData
        });
        return res;






