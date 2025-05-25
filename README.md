# Cross-Chain Integration Security Review Guideline

This guideline outlines the security review process for auditing projects integrating with cross-chain interoperability protocols such as Across, LayerZero, Wormhole, etc.

## Security Mindset

Adopt a skeptical and proactive approach:

* Assume nothing works as intended until proven otherwise through testing.
* Prioritize real-world validation over manual review alone, as cross-chain systems involve complex state interactions that are difficult to assess solely through code review.
* Focus on user experience: Identify pain points or usability issues affecting system adoption or security.
* Leverage challenges as opportunities: Deployment or configuration difficulties can deepen system understanding and uncover hidden issues.

## Procedure

Follow these steps to conduct a comprehensive security review for a cross-chain integration project:

1. **Deployment Scripts**
    * Check for existing deployment scripts in the project repository.
    * If none exist, create deployment scripts using Foundry (Forge). Use AI-assisted tools (e.g., Cursor) to accelerate script creation.
    * Deploy and verify contracts on block explorers (e.g., Etherscan) using a standardized process to streamline future engagements (see "Reusable Components" below).
2. **Set Up Cross-Chain Configuration**
    * Configure the deployed protocol (e.g., set up relayers, message channels, or gas parameters) to enable cross-chain communication.
    * Use pre-existing configuration templates for common protocols (e.g., LayerZero, Wormhole) to reduce setup time (see "Reusable Components" below).
3. **Test the Happy Path**
    * Write a script to execute a straightforward, successful cross-chain transaction (the "happy path").
    * Deploy and execute the transaction, debugging its behavior with Tenderly.
    * Share the transaction hashes with the client to demonstrate initial progress and validate the setup.
4. **Perform Manual Threat Modeling**
    * Analyze the codebase to understand its logic, state transitions, and interactions with the interoperability protocol.
    * Identify potential weak spots, such as:
        * Gas underpayment scenarios.
        * Refund mechanism reliability.
        * Latency or timing issues in cross-chain message delivery.
        * Encoding/decoding accuracy for cross-chain messages.
        * Off-chain handshake or configuration assumptions (e.g., relayer behavior).
    * Document assumptions and uncertainties about the system’s behavior.
5. **Test Edge Cases and Assumptions**
    * Design and execute transactions to test identified weak spots and edge cases, such as:
        * Underpaying gas for a cross-chain message and verifying delivery or failure.
        * Simulating delayed messages to assess impact on system state.
        * Testing refund mechanisms under various failure conditions.
        * Validating encoding/decoding processes with malformed or edge-case inputs.
        * Confirming off-chain infrastructure behavior (e.g., relayer responses).
    * Use Tenderly to debug and analyze transaction outcomes.

6. **Share Deliverables with the Client**
    * Provide the client with:
        * Deployment scripts used during the review.
        * Transaction hashes for happy path and edge-case tests.
        * A detailed report summarizing findings, including vulnerabilities, user experience issues, and recommendations.
    * Highlight how the testing process mirrors real-world usage, adding value beyond a standard code review.

## Benefits of This Approach

* **Deep System Understanding**: Deploying and testing the system reveals nuances in its behavior, such as deployment quirks or configuration challenges, that are not apparent in code alone.
* **User Experience Insights**: Interacting with the system as a user highlights pain points (e.g., complex parameter setup) that could affect usability or lead to misconfigurations.
* **Concrete Deliverables**: Sharing deployment scripts and transaction logs provides tangible evidence of the review process, differentiating the agency from competitors.

## Potential Pitfalls and Solutions

1. **Deployment Issues**
    * Problem: Contracts may fail to deploy due to configuration errors, missing dependencies, or chain-specific quirks.
    * Solution: Treat deployment challenges as learning opportunities. Document solutions for reuse in future engagements.
2. **Configuration Complexity**
    * Problem: Setting up cross-chain communication can be time-consuming and error-prone.
    * Solution: Develop reusable configuration templates for common protocols (e.g., Across, LayerZero). 
3. **Unverified Contracts**
    * Problem: Some interoperability protocols have unverified contracts on certain chains.
    * Solution: Check the interopeability protocol repositories for contract source code. This is actually a great opportunity to network and seek help from interop protocol engineers which we can contact to support us during the engagement. This adds value to the client and builds relationships. 

## Reusable Components
To streamline future engagements, maintain the following:
* **Configuration Templates**: Predefined scripts for setting up common interoperability protocols (e.g., Across, LayerZero, Wormhole) on popular blockchains.
* **Contract Verification Process**: A standardized script or .env file setup for verifying contracts on block explorers like Etherscan, Polygonscan, or Arbiscan.
* **Happy Path Scripts**: Generic scripts for executing standard cross-chain transactions, adaptable to specific projects.
