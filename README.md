# SMARTcontractfundME
This smart contract will allow buyers and sellers to exchange ETH and USD, JPY, GBP, EUR, NZD, CAD, CAD on the blockchain for a minimum and unlimited maximum.  

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract DataConsumerV3 {
    AggregatorV3Interface internal dataFeed;

    address[] public funders;
    mapping(address => uint256) public addressToAmountFunded;

    function fund() public payable{
        // assuming a function getConversionRate() which returns uint value
        uint conversionRate = getConversionRate();
        // assuming a constant minimum_USD_JPY_GBP_EUR_CAD_CHF
        uint minimum_USD_JPY_GBP_EUR_CAD_CHF = 1; 
        require(conversionRate >= minimum_USD_JPY_GBP_EUR_CAD_CHF, "didn't have enough ETH"); 
        funders.push(msg.sender);
        addressToAmountFunded[msg.sender] += msg.value; // correct the typo in variable name
    }

    function withdraw() public {  // corrected the function name
        // iterate through all funders
        for (uint256 funderIndex = 0; funderIndex < funders.length; funderIndex++){ // corrected typo in loop declaration and use .length for array
            // Add withdrawal logic here
        }
    }

    // assuming a function getPrice() which returns uint value
    function getPrice() public view returns(uint256) {
        (,int256 answer,,,) = dataFeed.latestRoundData();
        return uint256(answer);
    }
    
    function getConversionRate() public view returns(uint) {
        // Implementation for getConversionRate
    }
}
