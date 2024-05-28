# functions-and-errors

# ProductFactory Smart Contract

## Overview

The `ProductFactory` smart contract is designed to manage the production of products, tracking total products, adjusting production rates, and calculating total costs. It includes functions to set the production rate, produce products, and calculate the total cost based on the production rate and total products produced. The contract emits events to log significant actions and ensures validity using require, assert, and revert statements.

## Features

- **Set Production Rate:** Allows setting a production rate with a validation check.
- **Produce Products:** Facilitates the production of products with a validation check.
- **Calculate Total Cost:** Computes the total cost of production based on the production rate.
- **Event Logging:** Emits events for key actions for better traceability and transparency.

## Prerequisites

- **Solidity:** ^0.8.0

## Installation

To use this contract, you need to have a Solidity development environment set up. If you haven't already, install the following:

1. **Node.js and npm:** Install from [Node.js](https://nodejs.org/).
2. **Truffle or Hardhat:** For development, testing, and deployment of the smart contract.

## Usage

### Setting Production Rate

Set the production rate with validation to ensure it's greater than 10.

```solidity
function setProductionRate(uint rate) public {
    require(rate > 10, "Production rate must be greater than 10");
    productionRate = rate;
    emit ProductionRateAdjusted(rate);
}
```

### Producing Products

Produce products with validation to ensure the quantity is greater than 10.

```solidity
function produce(uint quantity) public {
    assert(quantity > 10);
    totalProducts += quantity;
    emit ProductProduced(quantity);
}
```

### Calculating Total Cost

Calculate the total cost based on the total products and the production rate. Reverts if the production rate is not set.

```solidity
function calculateTotalCost() public returns (uint) {
    if (productionRate == 0) {
        revert("Production rate not set. Set production rate before calculating total cost");
    }

    // Assume a cost of 5 units per product for simplicity
    totalCost = totalProducts * 5 / productionRate;
    emit TotalCostCalculated(totalCost);

    return totalCost;
}
```

## Event Logging

The contract emits the following events to log significant actions:

- `ProductProduced(uint indexed quantity)`: Emitted when products are produced.
- `ProductionRateAdjusted(uint indexed rate)`: Emitted when the production rate is set.
- `TotalCostCalculated(uint totalCost)`: Emitted when the total cost is calculated.

## Security Considerations

- **Validation Checks:** The contract uses require and assert statements to ensure valid inputs and states.
- **Revert on Errors:** The contract reverts transactions with appropriate error messages when necessary conditions are not met.
- **Event Emissions:** Key actions are logged through events to provide transparency and traceability.

## License

This project is licensed under the MIT License.
