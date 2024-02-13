# Cairo Smart Contract Auditing Checklist

My checklist to Cairo based smart contract auditing.

- [ ] Read specification and documentation of project. Identifying the SLOC.

- [ ] Run static analyzers ([Caracal](https://github.com/crytic/caracal)) and linting tools ([Amarna](https://github.com/crytic/amarna)) on the project to validate the security statically and style guide

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

- [ ] Look over the project's tests + code coverage and look deeper at areas lacking coverage
