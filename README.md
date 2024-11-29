# Functions and Errors

This Solidity program demonstrates the use of ERC20 tokens, along with minting, burning, and transferring tokens from one account to another.

## Description

The program features the minting, burning, and transferring of ERC20 tokens. The contract implements the `ERC20` and `Ownable` interfaces from [OpenZeppelin](https://github.com/OpenZeppelin). The user-defined `mint()` function allows the creation of ERC20 tokens to an account, and the `burn()` function burns tokens on the sender account. Lastly, the `transferTokens()` function transfers tokens from the sender address to a receiver address with a specified amount of tokens.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., CreateToken.sol). Copy and paste the following code into the file:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.0.0/contracts/token/ERC20/ERC20.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.0.0/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor(string memory name, string memory symbol) ERC20(name, symbol) {
        _mint(msg.sender, 100 * 10**uint(decimals()));
    }

    function mint(address to, uint256 amount) external onlyOwner {
        _mint(to, amount);
    }

    function burn(uint256 amount) external {
        _burn(msg.sender, amount);
    }

    function transferTokens(address _receiver, uint256 _amount) external {
        require(balanceOf(msg.sender) >= _amount, "You do not have enough tokens for this transaction");
        approve(msg.sender, _amount);
        transferFrom(msg.sender, _receiver, _amount);
    }
}
```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.13" or newer, and then click on the "Compile Token.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "MyToken" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the mint or burn function. You can also check the values of the public state variables by clicking on them.

## Authors

Adriane Gil Roa  


## License

This project is licensed under the MIT License - see the LICENSE file for details