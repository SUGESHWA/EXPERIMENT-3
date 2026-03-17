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
A luxury good (e.g., a Rolex watch) is registered on-chain.
<img width="1422" height="944" alt="image" src="https://github.com/user-attachments/assets/a2f82115-559f-430f-bb40-20069101f76a" />



Ownership is transferred at every checkpoint.
<img width="1404" height="988" alt="image" src="https://github.com/user-attachments/assets/b27b64e3-5465-44dc-a6b4-c1b618cc2ad0" />


Buyers can check the authenticity before purchasing.
<img width="1428" height="1001" alt="image" src="https://github.com/user-attachments/assets/41d13327-d30f-4e70-839b-1a68b8b57360" />


<img width="1417" height="1021" alt="image" src="https://github.com/user-attachments/assets/71512706-d413-4c80-b9b4-06933abb17c3" />

# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 
Thus a smart contract that tracks the supply chain of luxury goods ensuring authenticaly is executed sucessfully

