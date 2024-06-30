# Smart Contract for Error Handling
This contract is written in Solidity, a programming language designed for building smart contracts on the Ethereum blockchain.
# Description
This smart contract demonstrates the functionalities of a token called "Degen" (DGN) with a redemption system for a reward named "Kitty." It showcases essential error-handling mechanisms in Solidity using "require" statements. These ensure proper function execution and prevent unexpected behavior. A verified smart contract on Snowtrace.
## Getting Started
## Executing program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.21;

    import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
    import "@openzeppelin/contracts/access/Ownable.sol";

    contract Kitty is ERC20, Ownable {
        constructor() ERC20("Degen", "DGN") Ownable(msg.sender) {}

    struct RedeemedKittyFood {
        uint256 quantity;          
        uint256 KittyRedeemed;  
    }

    event KittyRedeemed(address indexed redeemer, uint256 quantity, uint256 KittyRedeemed);

    uint256 public KittyCost = 1; 

    mapping(address => RedeemedKittyFood[]) private RedeemedKittyFoods;

    
    function mint(address to, uint256 quantity) public onlyOwner {
        require(to != address(0), "Cannot mint to zero address");
        require(quantity > 0, "Kitty minting quantity must be greater than zero");
        _mint(to, quantity);
    }

    
    function burn(uint256 quantity) public {
        require(quantity > 0, "Kitty burning quantity must be greater than zero");
        _burn(_msgSender(), quantity);
    }

   
    function redeem(uint256 quantity) public {
        require(quantity > 0, "Kitty redeemed quantity must be greater than zero");
        uint256 cost = quantity * KittyCost;
        require(balanceOf(_msgSender()) >= cost, "Insufficient kitties");

       
        _burn(_msgSender(), cost);

       
        RedeemedKittyFoods[_msgSender()].push(RedeemedKittyFood({
            quantity: quantity,
            KittyRedeemed: cost
        }));

        emit KittyRedeemed(_msgSender(), quantity, cost);
    }

    
    function getRedeemedKittyFoods(address account) public view returns (RedeemedKittyFood[] memory) {
        require(account != address(0), "Query for zero address");
        return RedeemedKittyFoods[account];
    }

    
    function printRedeemedKitty(address account) public view returns (string memory) {
        require(account != address(0), "Query for zero address");
        RedeemedKittyFood[] memory items = RedeemedKittyFoods[account];
        require(items.length > 0, "No redeemed Kitty found");

        string memory result = "";
        for (uint i = 0; i < items.length; i++) {
            result = string(abi.encodePacked(
                result,
                "Redemption ", uintToString(i + 1), ": ", 
                "Quantity: ", uintToString(items[i].quantity), 
                " Kitty Redeemed: ", uintToString(items[i].KittyRedeemed), 
                "\n"
            ));
        }
        return result;
    }

    
    function uintToString(uint256 v) internal pure returns (string memory) {
        if (v == 0) {
            return "0";
        }
        uint256 digits;
        uint256 temp = v;
        while (temp != 0) {
            digits++;
            temp /= 10;
        }
        bytes memory buffer = new bytes(digits);
        while (v != 0) {
            digits -= 1;
            buffer[digits] = bytes1(uint8(48 + uint256(v % 10)));
            v /= 10;
        }
        return string(buffer);
    }

   
    function checkBalance(address account) public view returns (uint256) {
        require(account != address(0), "Query for zero address");
        return balanceOf(account);
    }

    
    function transferKitty(address from, address to, uint256 quantity) public {
        require(quantity > 0, "Transfer quantity must be greater than zero");
        require(from != address(0), "Cannot transfer from zero address");
        require(to != address(0), "Cannot transfer to zero address");

        if (from == _msgSender()) {
            _transfer(from, to, quantity);
        } else {
            uint256 currentAllowance = allowance(from, _msgSender());
            require(currentAllowance >= quantity, "Transfer quantity exceeds allowance");
            _approve(from, _msgSender(), currentAllowance - quantity);
            _transfer(from, to, quantity);
        }
    }
    }
To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.21" (or another compatible version), and then click on the "Compile Token.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "Kitty" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by errorRequire and erorRevert functions. Click on the smart contract in the left-hand sidebar, and select Metacraft in the environment. In Metmask add Fuji network. After that confirm transaction with metamask. Then deploy the contract. Once deployed, you can interact with the contract functions like mint, burn, and redeem through Remix's user interface. Must include the "require" statements to ensure valid inputs and prevent errors during execution. Run all the cases on test net and verify the contract in Snowtrace.

## License
This project is licensed under the MIT License.

Feel free to reach out for any questions or further improvements to this project.
