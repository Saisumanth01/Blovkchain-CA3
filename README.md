Q.2 The following contract tracks ownership of items in a supply chain. Identify and explain
the security vulnerabilities in this contract. Rewrite the vulnerable function(s) to enhance its
security, particularly against reentrancy and unauthorized access.

pragma solidity ^0.8.0;
contract SupplyChain {
struct Item {
uint id;
address owner;
}
mapping(uint => Item) public items;
function transferItem(uint itemId, address newOwner) public {
require(items[itemId].owner == msg.sender, "Not the owner");
items[itemId].owner = newOwner;
(bool sent, ) = newOwner.call{value: msg.value}("");
require(sent, "Transfer failed");
}
}
