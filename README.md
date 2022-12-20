# Smart-Contract-Auditing-Checklist-
My checklist to smart contract auditing.

- [ ] Gas Optimization checks
    - [ ] Cache read varibles in memory
    - [ ] Use `calldata` instead of `memory` if not modifying the function parameter passed
    - [ ] Don't call `view` function inside of another function
    - [ ] Use `++i` instead of `i++` (gas comsumption order `i+=1` > `i=i+1` > `i++` > `++i`). Same for `--i`
    - [ ] Use `unchecked` to not check for integer overflow and underflow if not required
    - [ ] Use `constant` and `immutable` for variables that don't change
    - [ ] Use `revert` instead of `require`
- [ ] Low level issues
- [ ] Non critical issues
- [ ] Medium level issues
- [ ] High level issues
- [ ] Critical issues
