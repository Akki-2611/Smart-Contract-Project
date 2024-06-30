# Smart Contract for Error Handling
This contract is written in Solidity, a programming language designed for building smart contracts on the Ethereum blockchain.
# Description
It showcases how to handle errors in Solidity smart contracts. This smart contract implements the require(), assert(), and revert() statements. It is essential for writing robust and secure smart contracts. By using these statements effectively, you can ensure proper error handling and prevent unexpected behavior in your code.
## Getting Started
## Executing program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

     // SPDX-License-Identifier: MIT

     pragma solidity ^0.8.13;

        contract Error_Handling {
        function errorRequire(uint _i) public pure {
            require(_i > 100, "Input must be greater than 100");
        }

        function errorRevert(uint _i) public pure {
            if (_i <= 100) {
                revert("Input must be greater than 100");
            }
        }

        uint public num;

        function errorAssert() public view {
            assert(num == 0);
        }
    }

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.13" (or another compatible version), and then click on the "Compile Error.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "HelloWorld" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by errorRequire and erorRevert functions. Click on the smart contract in the left-hand sidebar, and then click on the errorRequire, enter the value of errorRequire and errorRevert then click on the call function after that click on the "transact" button to execute the function. However, if _i is less than or equal to 100, the require statement throws an error. This error halts the function's execution and prevents any further code from running within errorRequire. The error message "Input must be greater than 100" is included for debugging purposes. If _i is less than or equal to 100, the revert statement is triggered. This also throws an error and halts the function's execution. The error message "Input must be greater than 100" is again provided for debugging. A slight difference from require is that the revert might offer a partial gas refund for computations done before the error occurred. If num is indeed equal to 0, the assertion holds true, and the function continues without errors. 
## License
This project is licensed under the MIT License.

Feel free to reach out for any questions or further improvements to this project
