
# A Developers Guide For Building & Implementing Consensus Algorithms On The Celo Blockchain:

## Table Of Contents:

- [A Developers Guide For Building & Implementing Consensus Algorithms On The Celo Blockchain](#a-developers-guide-for-building-&-implementing-consensus-algorithms-on-the-celo-blockchain)
    - [Table Of Contents](#table-of-contents)
    - [Introduction](#introdution)
    - [Pre-requisites](#perequisites)
    - [What is Proof-of-Stake (PoS) Consensus?](#what-is-proof-of-stake-pos-consensus)
    - [How Does PoS Consensus Work on the Celo Blockchain?](#how-does-pos-consensus-work-on-the-celo-blockchain)
    - [Creating a PoSI Validator on the Celo Blockchain](#creating-a-posi-validator-on-the-celo-blockchain)
    - [Writing a PoSI Validator Smart Contract](#writing-a-posi-validator-smart-contract)
    - [Building the dapp to interact with the contract:](#building-the-dapp-to-interact-with-the-contract)
        - [Step 1: New React app creation](#step-1-new-react-app-creation)
        - [Step 2: Install the Celo SDK](#step-2-install-the-celo-sdk)
        - [Step 3: Import the PoSI validator contract:](#step-3-import-the-posi-validator-contract)
        - [Step 4: Import the PoSI validator contract in the app](#step-4-import-the-posi-validator-contract-in-the-app)
        - [Step 5: Display the list of validators](#step-5-display-the-list-of-validators)
        - [Step 6: Add a form to add a validator](#step-6-add-a-form-to-add-a-validator)
        - [Step 7: Add a form to remove a validator](#step-7-add-a-form-to-remove-a-validator)
        - [Step 8: Final touches](#step-8-final-touches)
    - [Conclusion](#conclusion)        


## Introdution:

Blockchain technology heavily relies on the consensus mechanisms. They make it possible for the network to agree on the ledger's current state and guarantee that every node has a consistent copy of the blockchain. The PoS (Proof-of-Stake) consensus technique is used by the Celo blockchain to reach consensus. We will delve further into the PoS consensus mechanism in this tutorial and discover how it functions in relation to the Celo blockchain.

## Pre-requisites:

To make the most of this course, you need to have the following pre-requisites before we begin:

- Understanding of Blockchain Technology and it's working.
- Knowledge of Solidity programming language.
- Install [Node.js](https://nodejs.org/en/download) & [NPM](https://www.npmjs.com/package/download) 
- Basic overview of [React](https://react-cn.github.io/react/downloads.html) and its components.
That's it, let's dive in.

## What is Proof-of-Stake (PoS) Consensus?-

Some blockchain networks employ the Proof-of-Stake (PoS) consensus technique to reach consensus among network nodes. PoS is based on the idea of staking as opposed to Proof-of-Work (PoW) which calls for miners to carry out complex computational labor to verify transactions and add new blocks to the blockchain.

To take part in the consensus process, a certain quantity of cryptocurrency must be locked up as collateral, a practice which is known as staking. In a PoS system, validators are chosen based on their stake to add new blocks to the blockchain. Validators are chosen at random with greater odds of selection for those with greater stakes.

PoS has an edge over PoW since it uses less energy and is more scalable. PoS also makes it simpler for little people to participate in the consensus process because they don't require expensive mining equipment.

## How Does PoS Consensus Work on the Celo Blockchain?-

Proof-of-stake with identity (PoSI) is a variation of PoS consensus is utilized by the Celo blockchain. In PoSI, validators are chosen according to their stake and identity. This safeguard against Sybil attacks requires validators to be able to validate their identity using a phone number.

You must first lock up a particular number of CELO tokens as collateral in order to become a validator on the Celo network. This collateral acts as a security deposit to make sure validators act in the network's best interest. If a validator behaves maliciously, their collateral could be slashed which would result in them losing some of their CELO tokens.

Epoch rotation is the mechanism through which validators are chosen to add fresh blocks to the blockchain. Every so often, during an epoch, validators are chosen to examine transactions and add new blocks to the blockchain. The Celo network's current epoch lasts for 36 hours.

From the pool of validators who have opted into the consensus process, a fresh group of validators is selected at random for each epoch. Based on their stake and identification, validators are picked. A validator's chances of being picked increase with the number of CELO tokens they have invested.

Once a validator has been chosen to validate transactions and add new blocks to the blockchain, they must create and sign a block. The block must be signed by a minimum of two-thirds of the validators in order to be considered valid. This helps to ensure that the network is secure and that no single validator can control the network.

## Creating a PoSI Validator on the Celo Blockchain:

You must first set up a node and lock up a specified quantity of CELO tokens as collateral in order to become a validator on the Celo network. How to begin going is as follows:

- **Create a Celo node:** You must install the required software and set your node up so that it can join to the Celo network. The Celo manual has comprehensive instructions on how to set up a Celo node.

- **Acquire CELO tokens:** To become a validator on the Celo network, you'll need to lock up a certain amount of CELO tokens as collateral. You can acquire CELO tokens on a cryptocurrency exchange or through a peer-to-peer transaction.

- **Make a validator group:** You can make a validator group to improve your chances of being selected as a validator. A validator group is a collection of validators who combine efforts to raise their stake and raise their chances of getting chosen. You must establish a Smart Contract on the Celo network in order to form a validator group.

- **Register your validator:** You must register your validator on the Celo network after setting up your node and purchasing CELO tokens. You can do this by submitting a transaction to the network that contains the amount of CELO tokens you have placed as collateral, your validator's public key, and both.

- **Join the validator group by submitting a transaction to the network:** If you've created a validator group you must join it. By doing this, you can combine your efforts with those of other validators to improve your chances of being chosen.

## Writing a PoSI Validator Smart Contract:

To create a validator group on the Celo network, you'll need to write a Smart Contract that implements the PoSI validator logic. Here's an example of a PoSI validator smart contract written in Solidity:

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract PoSIValidator {

    address[] public validators;

    function addValidator(address validator) public {
        validators.push(validator);
    }

    function removeValidator(address validator) public {
        for (uint i = 0; i < validators.length; i++) {
            if (validators[i] == validator) {
                delete validators[i];
                break;
            }
        }
    }

    function getValidators() public view returns (address[] memory) {
        return validators;
    }
}
```

This Smart Contract defines a PoSI validator group that allows validators to be added and removed from the group. The `addValidator` function adds a validator to the group while the `removeValidator` function removes a validator from the group. The `getValidators` function returns a list of all the validators in the group.

## Building the dapp to interact with the contract:

Here is an illustration of how to create an app that communicates with the Smart Contract for the PoSI validator that we created in the earlier section. Consider creating a mobile application that enables users to examine a list of the PoSI validators in a group and add or remove validators from the group. Here is how to go about it:

### Step 1: New React app creation:

Run the following command in your terminal to start a new React app:

```bash
npx create-react-app my-app
```

This will create a new React app in a directory named `my-app`.

### Step 2: Install the Celo SDK:

We must install the Celo SDK in order to communicate with the Celo network. Start your terminal and type the following command:

```bash
npm install @celo/contractkit
```
This will install the Celo SDK in your app.

### Step 3: Import the PoSI validator contract:

We must import the PoSI validator Smart Contract into our app in order to interact with it. In the src directory, make a new file called PoSIValidator.js and add the following code:

```javascript
import { contractkit } from './celo';
import PoSIValidator from './contracts/PoSIValidator.json';

const contractAddress = '<your-contract-address-here>';

const PoSIValidatorContract = new contractkit.web3.eth.Contract(PoSIValidator.abi, contractAddress);

export const getValidators = async () => {
  const validators = await PoSIValidatorContract.methods.getValidators().call();
  return validators;
};

export const addValidator = async (validator) => {
  const accounts = await contractkit.web3.eth.getAccounts();
  const txObject = PoSIValidatorContract.methods.addValidator(validator);
  const tx = await contractkit.sendTransactionObject(txObject, { from: accounts[0] });
  return tx;
};

export const removeValidator = async (validator) => {
  const accounts = await contractkit.web3.eth.getAccounts();
  const txObject = PoSIValidatorContract.methods.removeValidator(validator);
  const tx = await contractkit.sendTransactionObject(txObject, { from: accounts[0] });
  return tx;
};
```
This code exports three functions that allow us to interact with the PoSI validator smart contract. The `getValidators` function retrieves the list of validators in the group, while the `addValidator` and `removeValidator` functions add and remove validators from the group, respectively.

### Step 4: Import the PoSI validator contract in the app:

Open the `App.js` file in the `src` directory and import the `PoSIValidator` component:

```javascript 
import PoSIValidator from './PoSIValidator';
```

### Step 5: Display the list of validators:

In the `PoSIValidator` component, we can use the `getValidators` function to retrieve the list of validators and display it to the user. Update the `PoSIValidator` component as follows:

```javascript
import { useState, useEffect } from 'react';
import { getValidators } from './PoSIValidator';

function PoSIValidator() {
  const [validators, setValidators] = useState([]);

  useEffect(() => {
    async function fetchValidators() {
      const validators = await getValidators();
      setValidators(validators);
    }
    fetchValidators();
  }, []);

  return (
    <div>
      <h2>Validators</h2>
      <ul>
        {validators.map((validator) => (
          <li key={validator}>{validator}</li>
        ))}
      </ul>
    </div>
  );
}

export default PoSIValidator;
```

This code uses the `useState` and `useEffect` hooks to fetch the list of validators when the component mounts and stores it in state using the setValidators function. The `useEffect` hook is used to make sure that the fetchValidators function is only called once when the component mounts, rather than on every re-render.

### Step 6: Add a form to add a validator:

To allow users to add a validator to the group, we can add a form that takes a validator address as input. Update the `PoSIValidator` component as follows:

```javascript
import { useState, useEffect } from 'react';
import { getValidators, addValidator } from './PoSIValidator';

function PoSIValidator() {
  const [validators, setValidators] = useState([]);
  const [validatorInput, setValidatorInput] = useState('');

  useEffect(() => {
    async function fetchValidators() {
      const validators = await getValidators();
      setValidators(validators);
    }
    fetchValidators();
  }, []);

  const handleAddValidator = async (event) => {
    event.preventDefault();
    await addValidator(validatorInput);
    setValidatorInput('');
    const validators = await getValidators();
    setValidators(validators);
  };

  return (
    <div>
      <h2>Validators</h2>
      <ul>
        {validators.map((validator) => (
          <li key={validator}>{validator}</li>
        ))}
      </ul>
      <form onSubmit={handleAddValidator}>
        <label>
          Add validator:
          <input type="text" value={validatorInput} onChange={(e) => setValidatorInput(e.target.value)} />
        </label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}

export default PoSIValidator;
```
This code adds a form that takes a validator address as input and calls the `addValidator` function when the form is submitted.

### Step 7: Add a form to remove a validator:

 To allow users to remove a validator from the group, we can add a form that takes a validator address as input. Update the `PoSIValidator` component as follows:

```javascript 
import { useState, useEffect } from 'react';
import { getValidators, addValidator, removeValidator } from './PoSIValidator';

function PoSIValidator() {
  const [validators, setValidators] = useState([]);
  const [validatorInput, setValidatorInput] = useState('');

  useEffect(() => {
    async function fetchValidators() {
      const validators = await getValidators();
      setValidators(validators);
    }
    fetchValidators();
  }, []);

  const handleAddValidator = async (event) => {
    event.preventDefault();
    await addValidator(validatorInput);
    setValidatorInput('');
    const validators = await getValidators();
    setValidators(validators);
  };

  const handleRemoveValidator = async (event) => {
    event.preventDefault();
    await removeValidator(validatorInput);
    setValidatorInput('');
    const validators = await getValidators();
    setValidators(validators);
  };

  return (
    <div>
      <h2>Validators</h2>
      <ul>
        {validators.map((validator) => (
          <li key={validator}>{validator}</li>
        ))}
      </ul>
      <form onSubmit={handleAddValidator}>
        <label>
          Add validator:
          <input type="text" value={validatorInput} onChange={(e) => setValidatorInput(e.target.value)} />
        </label>
        <button type="submit">Submit</button>
      </form>
      <form onSubmit={handleRemoveValidator}>
        <label>
          Remove validator:
          <input type="text" value={validatorInput} onChange={(e) => setValidatorInput(e.target.value)} />
        </label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}

export default PoSIValidator;
```

This code adds a form that takes a validator address as input and calls the `removeValidator` function when the form is submitted.

### Step 8: Final touches:

Now that our mock app is operational, we can make a few design and usability improvements. To style the PoSIValidator component, we can utilize CSS. 
Here is an illustration of how to style the component:

```javascript
import { useState, useEffect } from 'react';
import { getValidators, addValidator, removeValidator } from './PoSIValidator';
import './PoSIValidator.css';

function PoSIValidator() {
  const [validators, setValidators] = useState([]);
  const [validatorInput, setValidatorInput] = useState('');

  useEffect(() => {
    async function fetchValidators() {
      const validators = await getValidators();
      setValidators(validators);
    }
    fetchValidators();
  }, []);

  const handleAddValidator = async (event) => {
    event.preventDefault();
    await addValidator(validatorInput);
    setValidatorInput('');
    const validators = await getValidators();
    setValidators(validators);
  };

  const handleRemoveValidator = async (event) => {
    event.preventDefault();
    await removeValidator(validatorInput);
    setValidatorInput('');
    const validators = await getValidators();
    setValidators(validators);
  };

  return (
    <div className="PoSIValidator">
      <h2>Validators</h2>
      <ul>
        {validators.map((validator) => (
          <li key={validator}>{validator}</li>
        ))}
      </ul>
      <form onSubmit={handleAddValidator}>
        <label>
          Add validator:
          <input type="text" value={validatorInput} onChange={(e) => setValidatorInput(e.target.value)} />
        </label>
        <button type="submit">Submit</button>
      </form>
      <form onSubmit={handleRemoveValidator}>
        <label>
          Remove validator:
          <input type="text" value={validatorInput} onChange={(e) => setValidatorInput(e.target.value)} />
        </label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}

export default PoSIValidator;
```

And here's the CSS code for the `PoSIValidator` component:

```css
.PoSIValidator {
  font-family: Arial, sans-serif;
  margin: 20px;
}

h2 {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 10px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  font-size: 18px;
  margin-bottom: 10px;
}

label {
  display: block;
  margin-bottom: 10px;
}

input[type="text"] {
  font-size: 16px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button[type="submit"] {
  font-size: 16px;
  padding: 5px 10px;
  background-color: #008080;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button[type="submit"]:hover {
  background-color: #006666;
}
```

This CSS code gives the PoSIValidator component some fundamental styling to improve its appearance and user-friendliness.

That's all!! Using Solidity and React, we created a dummy app for a PoSI contract on the Celo blockchain. Of course, this is just a starting point and there are lots of ways we can enhance and expand on this program. Nevertheless, perhaps this lesson has provided you with a solid foundation for creating your own.

## Conclusion:

The PoS consensus algorithm and its operation in relation to the **Celo** blockchain have been discussed in this lesson. We've learnt how epoch rotation is utilized to keep the network safe and decentralized, how validators are chosen based on their stake and identity and how validators are selected. Additionally, we went over how to set up a Solidity Smart Contract to create a PoSI validator group and join the **Celo** network as a validator, we also built a very simple mock DApp to interact with the contract on a user friendly ground. Developers may create scalable and more effective blockchain apps on the **Celo** network by knowing the PoS consensus method.
