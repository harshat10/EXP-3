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

<img width="1905" height="1050" alt="Screenshot 2026-05-17 191809" src="https://github.com/user-attachments/assets/668336cf-5338-4a0c-bda6-746a7b145aff" />

Ownership is transferred at every checkpoint.

<img width="1913" height="1047" alt="Screenshot 2026-05-17 192146" src="https://github.com/user-attachments/assets/0d8c8d6a-0888-4e44-a0c9-2107d8172931" />

Buyers can check the authenticity before purchasing.

<img width="1918" height="1055" alt="Screenshot 2026-05-17 192224" src="https://github.com/user-attachments/assets/e612d16b-4e36-41a4-a1bc-b9fc62c6b7b4" />

# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 
Hence we implemented code for a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
