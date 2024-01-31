# Distributing amount rounding to zero

## Severity

High Risk

## Relevant GitHub Links

<https://github.com/Cyfrin/2023-08-sparkn/blob/0f139b2dc53905700dd29a01451b330f829653e9/src/Distributor.sol#L146>

## Summary

`_distribute` internal function is responsible for transferring the funds to winners. Sponsors add funds to the proxy contract before deployment of the proxy. Based on the percentage assigned by the organizer or owner and the total amount available in the proxy contract, the fund is distributed to winners selected by the organizer/owner.

## Vulnerability Details

Rounding down to zero vulnerability occurs when small numbers are not considered during calculation. Precision loss when small numbers are divided due to big numbers.

## Impact

If the sponsored amount is small (token amount ~ 1 wei) with 95% to one winner then zero tokens are transferred to the winner because rounding down to zero and 1 wei is sent to the stadium address. Also, in another case where the sponsored amount is 1000 wei with 0.01% to 95 winners, a similar thing happens where winners get 0 tokens, and 1000 wei tokens are sent to the stadium address (remaining amount).

## Tools Used

Manual + Foundry

```solidity
modifier setUpContestForJasonAndSentJpycv2Token(address _organizer) {
        vm.startPrank(factoryAdmin);
        bytes32 randomId = keccak256(abi.encode("Jason", "001"));
        proxyFactory.setContest(_organizer, randomId, block.timestamp + 8 days, address(distributor));
        vm.stopPrank();
        bytes32 salt = keccak256(abi.encode(_organizer, randomId, address(distributor)));
        address proxyAddress = proxyFactory.getProxyAddress(salt, address(distributor));
        vm.startPrank(sponsor);
        MockERC20(jpycv2Address).transfer(proxyAddress, 1000 wei);
        vm.stopPrank();
        // console.log(MockERC20(jpycv2Address).balanceOf(proxyAddress));
        assertEq(MockERC20(jpycv2Address).balanceOf(proxyAddress), 1000 wei);
        _;
    }

function createData() public view returns (bytes memory data) {
        address[] memory tokens_ = new address[](1);
        tokens_[0] = jpycv2Address;
        address[] memory winners = new address[](9500);
        for(uint i;i <9500; i++) {
            winners[i] = vm.addr(i+15); // 9500 winners
        }
        uint256[] memory percentages_ = new uint256[](9500);
        for(uint i;i <9500; i++) {
            percentages_[i] = 1; // 0.01%
        }
        data = abi.encodeWithSelector(Distributor.distribute.selector, jpycv2Address, winners, percentages_, "");
    }

function testSucceedsIfAllConditionsMet1() public setUpContestForJasonAndSentJpycv2Token(organizer) {
        // before
        assertEq(MockERC20(jpycv2Address).balanceOf(user1), 0 ether);
        assertEq(MockERC20(jpycv2Address).balanceOf(stadiumAddress), 0 ether);

        bytes32 randomId_ = keccak256(abi.encode("Jason", "001"));
        bytes memory data = createData();

        vm.warp(16 days);
        vm.startPrank(factoryAdmin);
        proxyFactory.deployProxyAndDistributeByOwner(organizer, randomId_, address(distributor), data);
        vm.stopPrank();

        console2.log(MockERC20(jpycv2Address).balanceOf(user1));
        console2.log(MockERC20(jpycv2Address).balanceOf(stadiumAddress));
        // after
        // assertEq(MockERC20(jpycv2Address).balanceOf(user1), 9500 ether);
        // assertEq(MockERC20(jpycv2Address).balanceOf(stadiumAddress), 500 ether);
    }
```

## Recommendations

Consider including a check if the calculated `amount` is zero before `safeTransfer` of tokens to the winners in `_distribute` function.
