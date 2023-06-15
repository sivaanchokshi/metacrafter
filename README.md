# metacrafter
assignment for metacrafters

READ ME
This Solidity contract implements an ERC20 token, which is a standard interface for fungible tokens on the Ethereum blockchain. The contract includes functions to mint new tokens and burn existing tokens, as well as track the balances of token holders.

## How it works

1. Token Name, Token Abbreviation, and Total Supply
   - The contract includes public variables to store the name, symbol (abbreviation), and total supply of the token.

2. Address-to-Balance Mapping
   - The contract maintains a mapping of addresses to token balances using the `balances` mapping.

3. Mint Function
   - The `mint` function allows the contract owner to create new tokens and assign them to a specified address.
   - Parameters: `recipient` (address) - the recipient address to receive the minted tokens, `value` (uint256) - the amount of tokens to mint.
   - The function increases the total supply by the specified amount and adds it to the balance of the recipient address.

4. Burn Function
   - The `burn` function enables token holders to destroy their own tokens.
   - Parameters: `account` (address) - the address of the token holder who wants to burn tokens, `value` (uint256) - the amount of tokens to burn.
   - The function decreases the total supply by the specified amount and deducts it from the balance of the token holder's address.
   - The function includes conditionals to ensure that the token holder's balance is greater than or equal to the amount being burned.

CODE 

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyToken {
    string public name;
    string public symbol;
    uint256 public totalSupply;
    mapping(address => uint256) balances;

    constructor(string memory _name, string memory _symbol, uint256 _totalSupply) {
        name = _name;
        symbol = _symbol;
        totalSupply = _totalSupply;
        balances[msg.sender] = _totalSupply;
    }

    function mint(address recipient, uint256 value) public {
        totalSupply += value;
        balances[recipient] += value;
    }

    function burn(address account, uint256 value) public {
        require(balances[account] >= value, "Insufficient balance");
        totalSupply -= value;
        balances[account] -= value;
    }
    
    function balanceOf(address account) public view returns (uint256) {
        return balances[account];
    }
}
