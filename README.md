# evm-gas-fee-fix

### smart contract example
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract Donate {
    address payable public owner;
    address payable public charityOrganization = payable(0x62Bc5A67eFc9778a85c86aE5CaF218f6cA76b519);
    
    constructor() {
        owner = payable(msg.sender);
    }
    
    function buyMeACoffee() public payable {
        require(msg.value == 0.001 ether, "You should send exactly 0.001 SWTR.");
        owner.transfer(msg.value);
    }
    
    function plantATree() public payable {
        require(msg.value > 0, "You should send more than 0 SWTR.");
        charityOrganization.transfer(msg.value);
    }
}
```

### assigning the following variables will help in solving the problem. values may vary according to network variables.
```
const BLOCK_GAS_LIMIT: u64 = 75_000_000;
const WEIGHT_MILLISECS_PER_BLOCK: u64 = 2000;
```

```
pub BlockGasLimit: U256 = U256::from(BLOCK_GAS_LIMIT);
pub WeightPerGas: Weight = Weight::from_ref_time(fp_evm::weight_per_gas(BLOCK_GAS_LIMIT, WEIGHT_MILLISECS_PER_BLOCK));
```
