# Smart-Contract-Auditing-Checklist
My checklist to smart contract auditing.

- [ ] Read specification and documentation of project

- [ ] Run static analyzers (Slither) on the project

- [ ] Maunal analyzes
    - [ ] Gas Optimization checks
        - [ ] Cache read varibles in memory
        - [ ] Use `calldata` instead of `memory` if not modifying the function parameter passed
        - [ ] Don't call `view` function inside of another function
        - [ ] Use `++i` instead of `i++` (gas comsumption order `i+=1` > `i=i+1` > `i++` > `++i`). Same for `--i`
        - [ ] Use `unchecked` to not check for integer overflow and underflow if not required
        - [ ] Use `constant` and `immutable` for variables that don't change
        - [ ] Use `revert` instead of `require`
        - [ ] Create custom errors rather than `revert()`/`require()` strings to save gas
        - [ ] Put `require` statements on top in a function 
        - [ ] Use `indexed` if less than three arguments are there in events for faster access
        - [ ] Use `!= 0` instead of `> 0` for unsigned integer comparison
        - [ ] `internal` functions not called by the contract should be removed
        - [ ] Cache array length outside of loop
        - [ ] Use `bytes` instead of `string`. Bytes constants are more efficient than string constants
        - [ ] Use external function modifier.
    
    - [ ] Informational
        - [ ] NatSpec comments should be increased in contracts (https://docs.soliditylang.org/en/v0.8.15/natspec-format.html)
        - [ ] Check undocumented parameters
        - [ ] Events emitted for critical state changes for tracking in off-chain.

    - [ ] Low risk issues
        - [ ] `abi.encode()` instead of `abi.encodePacked()` for dynmaic types when passing to `keccak256()`
        - [ ] Check the modifiers whether any state changes happening.
        - [ ] New version of Solidity
        - [ ] Using non-vulnerable version of openzepplin dependencies
        - [ ] zero address check
        

    - [ ] Non critical issues
        - [ ] Check return values of `approve()` in ERC20 implementations
        - [ ] Use the latest version of OpenZeppelin from dependencies
        - [ ] Missing error `message` in require statement
        

    - [ ] Medium risk issues
        - [ ] Check for integer underflow and overflow 
        - [ ] Verify transfer and transferFrom return values - Use safeERC20 wrappers
        - [ ] Check the parameter orderings
        - [ ] Avoid using extcodesize to check for Externally Owned Accounts.

    - [ ] High risk issues

    - [ ] Critical issues
        - [ ] Check for possible re-entrancy - add OZ reentrancy guard 
        - [ ] Input Validations - Use SafeMath
        - [ ] Error Handlings - Check error code revert if necessary
