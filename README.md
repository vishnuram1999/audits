# Smart-Contract-Auditing-Checklist

My checklist to smart contract auditing.

- [ ] Read specification and documentation of project

- [ ] Manual analyzes

  - [ ] Gas Optimization checks

    - [ ] Cache read variables in memory
    - [ ] Use `calldata` instead of `memory` if not modifying the function parameter passed
    - [ ] Don't call `view` function inside of another function
    - [ ] Use `++i` instead of `i++` (gas consumption order `i+=1` > `i=i+1` > `i++` > `++i`). Same for `--i`.
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
    - [ ] Use full 256 bit types unless packing with other variables.

  - [ ] Informational checks

    - [ ] Document variables, structs, functions, modifiers, events, contract purpose using Natspec
    - [ ] NatSpec comments should be increased in contracts (https://docs.soliditylang.org/en/v0.8.15/natspec-format.html)
    - [ ] Check undocumented parameters
    - [ ] Events emitted for critical state changes for tracking in off-chain.
    - [ ] Check return values of `approve()` in ERC20 implementations
    - [ ] Use the latest version of OpenZeppelin from dependencies
    - [ ] Missing error `message` in require statement, also check whether it is relevant.

  - [ ] Low severity issue checks

    - [ ] `abi.encode()` instead of `abi.encodePacked()` for dynamic types when passing to `keccak256()`
    - [ ] Check the modifiers whether any state changes happening.
    - [ ] New version of Solidity
    - [ ] Using non-vulnerable version of Openzeppelin dependencies
    - [ ] Zero address check
    - [ ] Race condition on ERC20 approval
    - [ ] Risk of Renounce Ownership in Ownable contracts
    - [ ] Any hardcoded addresses - causes no future updates
    - [ ] Whether any critical Address Changes (Should Use Two-step Procedure)
    - [ ] Use `Ownable2StepUpgradeable` instead of `OwnableUpgradeable` contract
    - [ ] `solmate`'s `SafeTransferLib` doesn't check whether the ERC20 contract exists
    - [ ] Check loss of precision due to rounding

  - [ ] Medium severity issue checks

    - [ ] Check for integer underflow and overflow
    - [ ] Verify transfer and transferFrom return values - Use safeERC20 wrappers
    - [ ] Check the parameter orderings
    - [ ] Avoid using extcodesize to check for Externally Owned Accounts
    - [ ] Missing function arguments verification
    - [ ] Using transfer() or send() function to send eth to contract address? - instead use call() to send data or value
    - [ ] Centralization risk, whether only one owner has access to major functions?

  - [ ] High severity issue checks

    - [ ] First pool depositor front-running
    - [ ] Check for possible re-entrancy - add OZ re-entrancy guard
    - [ ] Input Validations - Use SafeMath
    - [ ] Error Handlings - Check error code revert if necessary
    - [ ] Any timestamp dependance for state changes

- [ ] Glance over the project's tests + code coverage and look deeper at areas lacking coverage

- [ ] Do another review from the perspective of every actor in the threat model.

- [ ] Run static analyzers (Slither) on the project

- [ ] Run symbolic execution tools (Manticore, Mythril) for detecting vulnerabilities
