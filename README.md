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
