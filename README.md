# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
The manufacturer records product creation details on-chain.


The product moves through different supply chain checkpoints.


The ownership of the product can be transferred securely.


Buyers can verify the product’s authenticity.


# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
<img width="1920" height="1200" alt="Screenshot (44)" src="https://github.com/user-attachments/assets/4dfebf7b-de91-4c6c-864d-1a397a7ca06a" />


<img width="1920" height="1200" alt="Screenshot (45)" src="https://github.com/user-attachments/assets/2a4fea9b-d58b-4057-9262-88e24efeba33" />


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 
Thus a smart contract that tracks the supply chain of luxury goods ensuring authenticaly is executed sucessfully

