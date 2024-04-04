# Solidity Smart Contract Auditing Checklist

My checklist to Solidity based smart contract auditing.

- [ ] Read specification and documentation of project. Identifying the SLOC.

- [ ] Use a Visualizer to inspect the contracts in the protocol like [Surya](https://github.com/ConsenSys/surya).

- [ ] Run static analyzers ([Slither](https://crytic.github.io/slither/slither.html)) and linting tools([solhint](https://github.com/protofire/solhint)) on the project to validate the security statically and style guide

- [ ] Write fuzz and invariant tests using Foundry, [Echidna](https://github.com/crytic/echidna) or [Medusa](https://github.com/crytic/medusa)

- [ ] Run symbolic execution tools ([Manticore](https://github.com/trailofbits/manticore), [Mythril](https://github.com/ConsenSys/mythril), [Halmos](https://github.com/a16z/halmos)) for detecting vulnerabilities

- [ ] Start a mutation testing campaign using [slither-mutate](https://github.com/crytic/slither/tree/master/slither/tools/mutator) or [universalmutator](https://github.com/agroce/universalmutator) to evaluate the test suite built

- [ ] Building a Threat Model
  - [ ] what is the business objective of the protocol?
  - [ ] Who is the threat actor?
  - [ ] What can go wrong?
  - [ ] What is the impact and the likelihood of a threat being carried out?
  - [ ] What can be done to mitigate the risks?
  - [ ] What within the protocol has value in the market?
  - [ ] In what case can protocol/users lose money?
  - [ ] Identify the potential goals of an attacker

- [ ] Manual analyzes

  - [ ] Gas Optimization checks

    - [ ] Cache read variables in memory
    - [ ] Use `calldata` instead of `memory` if not modifying the function parameter passed
    - [ ] Don't call `view` function inside of another function
    - [ ] Use `++i` instead of `i++` (gas consumption order `i+=1` > `i=i+1` > `i++` > `++i`). Same for `--i`.
    - [ ] Use `unchecked` to not check for integer overflow and underflow if not required
    - [ ] Add `unchecked` {} for subtractions where the operands cannot underflow
    - [ ] Use `constant` and `immutable` for variables that don't change
    - [ ] Use `revert` instead of `require`
    - [ ] Create custom errors rather than `revert()`/`require()` strings to save gas
    - [ ] Put `require` statements on top in a function
    - [ ] Use `indexed` if less than three arguments are there in events for faster access
    - [ ] Use `!= 0` instead of `> 0` for unsigned integer comparison (<0.8.12 it was cheaper)
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
    - [ ] Remove public visibility from constant variables
    - [ ] Emitting storage values instead of memory calldata ones does cost more gas
    - [ ] `MULMOD` opcode is cheaper than `MUL` and `MOD` opcodes when used together
    - [ ] Use double if statements instead of &&
    - [ ] Don’t call a function when initializing an immutable variable
    - [ ] Use assembly to write address storage values
    - [ ] Sort Solidity operations using short-circuit mode
    - [ ] Instead of checking a uint is odd using % 2, check the last bit with & uint(1).
    - [ ] Timestamps don't need to be larger than uint48. You can probably pack them with something else.
    - [ ] Make constructors payable even if you don't deploy with ETH. This will reduce the deployment cost.
    - [ ] If a variable never changes after construction, make sure it is immutable. This is one of the most impactful things you can do for gas
    - [ ] If a user needs to make several calls to a smart contract, give them a mechanism to "batch up" the transactions into one transaction. Compound calls this a "bulker" others call it a "multicall." Just initiating a transaction costs 21,000 gas, (roughly $3 right now), so your customers will appreciate not having to do multiple transactions!
    - [ ] Change your imported libraries to Solady. These libraries are gas optimized and often have the same interface as more well-known libraries.
    - [ ] Initialize the return variable in the function header itself to save gas (Ex: `function ArraySum() public returns (uint256 sum) {`)
    - [ ] Don’t compare boolean expressions to boolean literals
    - [ ] Multiplication/division by two should use bit shifting

  - [ ] Informational checks
  
    - [ ] Document variables, structs, functions, modifiers, events, contract purpose using [NatSpec](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html).
    - [ ] NatSpec comments should be increased in contracts.
    - [ ] Check undocumented parameters
    - [ ] Events emitted for critical state changes for tracking in off-chain.
    - [ ] Check return values of `approve()` in ERC20 implementations
    - [ ] Use the latest version of OpenZeppelin from dependencies
    - [ ] Missing error `message` in require statement, also check whether it is relevant.
    - [ ] Follow solidity [naming conventions](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#naming-conventions)
    - [ ] Use of `string.concat()` instead of `abi.encodePacked()`
    - [ ] Mixed use of `require` and `revert`
    - [ ] Remove unused imports
    - [ ] Use `_` to separate the zeros in numbers
    - [ ] Lack of Brace Spacing (Ex: use { statement }instead of {statement})

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
    - [ ] Deleting arrays that others can add to is also an denial of service vector
    - [ ] use `_grantRole()` instead of the deprecated `_setupRole()` when using OpenZeppelin's `AccessControl.sol`
    - [ ] USE DISABLEINITIALIZERS TO PREVENT FRONT-RUNNING ON THE INITIALIZE FUNCTION
    - [ ] Use encodeCall instead of encodeWithSignature to provide type checking
    - [ ] The call `abi.encodeWithSignature` is not safe from typographical errors
    - [ ] Contracts are vulnerable to fee-on-transfer accounting-related issues
    - [ ] Function calls within `for` loops
    - [ ] In production, foundry assertions should not be used


  - [ ] Medium severity issue checks

    - [ ] Check for integer underflow and overflow
    - [ ] Verify `transfer` and `transferFrom` return values - Use `safeERC20` wrappers
    - [ ] Check the parameter orderings
    - [ ] Avoid using extcodesize to check for Externally Owned Accounts
    - [ ] Missing function arguments verification
    - [ ] Using `transfer` or `send` function to send eth to contract address? - instead use `call` to send data or value
    - [ ] Centralization risk, whether only one owner has access to major functions?
    - [ ] [Must approve 0 first](https://audit-hero.com/finding/cf63054b)
    - [ ] Hardcoding gas costs should be avoided
    - [ ] Better to use more than one oracle feed for feeds to avoid single point of failure
    - [ ] Make sure the first value (default state) in a enum is set correct
    - [ ] Delegatecall external contract missing existence check
    - [ ] [Function Clashing Vulnerability](https://proxies.yacademy.dev/pages/security-guide/#function-clashing-vulnerability)
    - [ ] Use _msgSender() instead of msg.sender in case protocol supports meta-transactions
    - [ ] Instead of `a/b > c/d` it is often better to use `a*d > c*b`
    - [ ] To avoid overflow/underflow it is better to do all calculations in the uint256 type (type conversions and use SafeCast)
    - [ ] No storage `__gap` variable for upgradable contract might lead to storage slot collision
    - [ ] Check the size of `__gap`s in each upgradable logic contract to maintain the code
    - [ ] Always use the upgradeable versions of the openzeppelin contracts if using UUPSUpgradeable.
    - [ ] Use `initializer` modifier in the `initialize` function

  - [ ] High severity issue checks

    - [ ] First pool depositor front-running
    - [ ] Check for possible re-entrancy - add OZ re-entrancy guard
    - [ ] Input Validations - Use SafeMath
    - [ ] Error Handlings - Check error code revert if necessary
    - [ ] Any timestamp dependance for state changes
    - [ ] [EIP-4626 Inflation Attack](https://ethereum-magicians.org/t/address-eip-4626-inflation-attacks-with-virtual-shares-and-assets/12677)
    - [ ] [Gas Grieving Attack](https://consensys.github.io/smart-contract-best-practices/attacks/griefing/)
    - [ ] [Unexpected Callback](https://github.com/kadenzipfel/smart-contract-vulnerabilities/blob/master/vulnerabilities/unprotected-callback.md)
    - [ ] [Risk](https://samczsun.com/the-dangers-of-surprising-code/) of using the `safe` functions of ERC token contracts while executing `Receiver` functions.
    - [ ] [Delegatecall with Selfdestruct Vulnerability](https://proxies.yacademy.dev/pages/security-guide/#delegatecall-with-selfdestruct-vulnerability)
    - [ ] Use `_init` functions of inheriting contract in the `initialize` function of impl contract.
    - [ ] Always override the `_authorizeUpgrade` function and add `onlyOwner` modifier if using UUPS upgrade pattern.

- [ ] Look over the project's tests + code coverage and look deeper at areas lacking coverage
