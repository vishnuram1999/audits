# Smart-Contract-Auditing-Checklist

My checklist to smart contract auditing.

- [ ] Read specification and documentation of project

- [ ] Use a Visualizer to inspect the contracts in the protocol like [Surya](https://github.com/ConsenSys/surya).

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
    - [ ] Splitting `require` statements that use && saves gas.
    - [ ] State variables can be packed into fewer storage slots.
    - [ ] Use scratch space for keccak.
    - [ ] No Need to Allocate Unused Variable.
    - [ ] Use basis points for ratios.
    - [ ] Skip initializing default values.
    - [ ] Non-strict inequalities are cheaper than strict ones
    - [ ] Usage of `uint8` may increase gas cost
    - [ ] Use bytesN instead of bytes[]
    - [ ] Inline a modifier that’s only used once.
    - [ ] Inverting the condition of an [if-else-statement](https://gist.github.com/IllIllI000/44da6fbe9d12b9ab21af82f14add56b9) wastes gas.
    - [ ] [Consider having short revert strings.](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#consider-having-short-revert-strings)

  - [ ] Informational checks

    - [ ] Document variables, structs, functions, modifiers, events, contract purpose using [NatSpec](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html).
    - [ ] NatSpec comments should be increased in contracts.
    - [ ] Check undocumented parameters
    - [ ] Events emitted for critical state changes for tracking in off-chain.
    - [ ] Check return values of `approve()` in ERC20 implementations
    - [ ] Use the latest version of OpenZeppelin from dependencies
    - [ ] Missing error `message` in require statement, also check whether it is relevant.
    - [ ] Follow solidity [naming conventions](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#naming-conventions)
    - [ ] Use of `bytes.concat()` instead of `abi.encodePacked()`
    - [ ] Mixed use of `require` and `revert`
    - [ ] Remove unused imports

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
    - [ ] Check loss of precision due to rounding.
    - [ ] Monitoring the third party dependencies.
    - [ ] Direct usage of `ecrecover` allows signature malleability (use [OpenZeppelin's ECDSA library](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/cryptography/ECDSA.sol))
    - [ ] Hardcoding chainID is error-prone

  - [ ] Medium severity issue checks

    - [ ] Check for integer underflow and overflow
    - [ ] Verify `transfer` and `transferFrom` return values - Use `safeERC20` wrappers
    - [ ] Check the parameter orderings
    - [ ] Avoid using extcodesize to check for Externally Owned Accounts
    - [ ] Missing function arguments verification
    - [ ] Using `transfer` or `send` function to send eth to contract address? - instead use `call` to send data or value
    - [ ] Centralization risk, whether only one owner has access to major functions?
    - [ ] [Must approve 0 first](https://audit-hero.com/finding/cf63054b)

  - [ ] High severity issue checks

    - [ ] First pool depositor front-running
    - [ ] Check for possible re-entrancy - add OZ re-entrancy guard
    - [ ] Input Validations - Use SafeMath
    - [ ] Error Handlings - Check error code revert if necessary
    - [ ] Any timestamp dependance for state changes
    - [ ] [EIP-4626 Inflation Attack](https://ethereum-magicians.org/t/address-eip-4626-inflation-attacks-with-virtual-shares-and-assets/12677)
    - [ ] [Gas Grieving Attack](https://consensys.github.io/smart-contract-best-practices/attacks/griefing/)

- [ ] Look over the project's tests + code coverage and look deeper at areas lacking coverage

- [ ] Do another review from the perspective of every actor in the threat model

- [ ] Run static analyzers ([Slither](https://github.com/crytic/slither)) and linting tools([solhint](https://github.com/protofire/solhint)) on the project to validate teh security and style guide

- [ ] Run symbolic execution tools ([Manticore](https://github.com/trailofbits/manticore), [Mythril](https://github.com/ConsenSys/mythril), [Halmos](https://github.com/a16z/halmos)) for detecting vulnerabilities
