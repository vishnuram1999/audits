# [G-01] `_bio` length check is incorrect in `Bio.sol`

Based on the given `README`, bio should be shorter than 200 characters not shorter than or equal to 200 characters. But the check in `mint` function is incorrect. Instead of `bytes(_bio).length >= 200` it is `bytes(_bio).length > 200`.

Changing this will also save gas from 705 to 699 in `mint` function

## Line Index

<https://github.com/code-423n4/2023-03-canto-identity/blob/077372297fc419ea7688ab62cc3fd4e8f4e24e66/canto-bio-protocol/src/Bio.sol#L123>

## Recommendation

Change the if statement like below

`if (bytes(_bio).length == 0 || bytes(_bio).length >= 200) revert InvalidBioLength(bytes(_bio).length);`