# Smart-Contract-Auditing-Checklist
My checklist to smart contract auditing.

- [ ] Gas Optimization checks
    - [ ] Cache read varibles in memory
    - [ ] Use `calldata` instead of `memory` if not modifying the function parameter passed
    - [ ] Don't call `view` function inside of another function
    - [ ] Use `++i` instead of `i++` (gas comsumption order `i+=1` > `i=i+1` > `i++` > `++i`). Same for `--i`
    - [ ] Use `unchecked` to not check for integer overflow and underflow if not required
    - [ ] Use `constant` and `immutable` for variables that don't change
    - [ ] Use `revert` instead of `require`
    - [ ] Put `require` statements on top in a function 
    - [ ] Use `indexed` if less than three arguments are there in events
    - [ ] Use `!= 0` instead of `> 0` for unsigned integer comparison
    - [ ] `internal` functions not called by the contract should be removed
    - [ ] Cache array length outside of loop

- [ ] Low level issues

- [ ] Non critical issues

- [ ] Medium level issues

- [ ] High level issues

- [ ] Critical issues
