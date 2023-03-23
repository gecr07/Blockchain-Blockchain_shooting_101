# Blockchain-Blockchain_shooting_101


## Code os Solution.js

```
const Web3 = require('web3');
const web3 = new Web3('http://104.248.169.232:30464'); 

const account = web3.eth.accounts.privateKeyToAccount('0xe8383de9fc48e57c3f7ba923c82d69ff729cd02cee86e23ab219bf721033710e');
 
const contractAddress = '0x8eB9A08F340067CaB4f58a9777e7fB6bc3Ced471';

const contractABI = [{
  inputs: [{
    internalType: 'uint256',
    name: 'value',
    type: 'uint256'
  }],
  name: 'updateSensors',
  outputs: [],
  stateMutability: 'nonpayable',
  type: 'function'
},
{
  inputs: [],
  name: 'updated',
  outputs: [{
    internalType: 'bool',
    name: '',
    type: 'bool'
  }],
  stateMutability: 'view',
  type: 'function'
}];

const contract = new web3.eth.Contract(contractABI, contractAddress);

const functionAbi = contractABI.find(element => element.name === 'updateSensors');
const functionArguments = [10]; // Valor del argumento a enviar

const encodedFunction = contract.methods[functionAbi.name](...functionArguments).encodeABI();

const txObject = {
  from: account.address,
  to: contractAddress,
  gas: 100000,
  data: encodedFunction
};

web3.eth.accounts.signTransaction(txObject, account.privateKey)
  .then(signedTx => {
    web3.eth.sendSignedTransaction(signedTx.rawTransaction)
      .on('receipt', console.log);
  })
  .catch(console.error);

```




















