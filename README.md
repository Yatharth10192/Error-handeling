# Error-handeling
In this project we are writing the smart contract that implements the functions as given in the question.
# Description
In this project we are writing the smart contract that implements three functions require(), assert(), and revert(). We have created the function to deposit  either into the contract. We have used require() to check for the valid deposit amount i.e. greater than 0. Then we have function to withdraw ether from the contract and we have used the require() function to ensure the caller is the owner and also to check for the sufficient balance. We also have the function to demonstrate the use of revert with custom error message. In the whole project we should ensure that only the owner can reset the balance.

# Getting started
# Installing
We have used online Ethereum IDE for this project.

# Executing program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/. After that create a file and write your code.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ErrorHandling {
    
    address public owner;
    uint256 public balance;
    
    constructor() {
        owner = msg.sender;
        balance = 0;
    }
    
    // Function to deposit ether into the contract

    function deposit() public payable {
        // Using require() to check for a valid deposit amount

        require(msg.value > 0, "Deposit amount must be greater than zero");
        
        balance += msg.value;
    }
    
    // Function to withdraw ether from the contract

    function withdraw(uint256 amount) public {
        // Using require() to ensure the caller is the owner

        require(msg.sender == owner, "Only the owner can withdraw funds");
        // Using require() to check sufficient balance

        require(balance >= amount, "Insufficient balance");
        
        balance -= amount;
        payable(owner).transfer(amount);
    }
    
    // Function to demonstrate the use of assert()

    function checkInvariant() public view {
        // Using assert() to check an invariant condition

        assert(balance >= 0);
    }
    
    // Function to demonstrate the use of revert() with custom error message

    function resetBalance() public {
        // Only the owner can reset the balance
        
        if (msg.sender != owner) {
            revert("Only the owner can reset the balance");
        }
        
        balance = 0;
    }
}

After this compile the code and then deploy it. After deploying it we can test different functions i.e. deposit, withdraw and check balance etc. The errors we encounter can give us great insights about error handeling.

# Help
For any help in the code we can take helpof the debug option in the compiler.

# Authors
Yatharth Sharma
yatharths10192@gmail.com
9350677109

# Licence
This project is licensed under the MIT License - see the LICENSE file for details
