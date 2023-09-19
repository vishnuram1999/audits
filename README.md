# Blockchain Auditing Service

## Introduction

Welcome to my smart contract security auditing service! As blockchain technology continues to grow and become more integrated into various industries, the security of smart contracts becomes increasingly important. With my expertise and experience in smart contract auditing, I am here to help you ensure that your smart contracts are secure and free from vulnerabilities.

My auditing process involves a comprehensive analysis of the code to identify any potential security risks and vulnerabilities. I use industry-standard tools and techniques to thoroughly test your smart contracts and provide you with a detailed report of any findings.

My goal is to help you identify and address any security issues before they can be exploited, minimizing the risks and protecting your business from potential financial losses or reputational damage.

I understand the importance of maintaining confidentiality and will treat your information with the utmost discretion. I am committed to providing you with reliable, professional, and efficient service, ensuring that you can confidently deploy secure smart contracts.

Reach out to me on Twitter [@Vishnuram73](https://twitter.com/Vishnuram73). Let's discuss. 

## Auditing Process

To get the best out of the each step in the following audit process is through interacting with the project developers and making sure I understand the project clearly.  

1. Initial Assessment: A preliminary review of the protocol to understand its functionalities, architecture, and design. Determining the scope of the audit, dependencies, and SLOC of the smart contracts.

2. Threat Model: Buidling a threat model based on the protocol's actors and their allowed actions. 

3. Static Analysis: In this step I use industry-standard tools (Like Slither, Mythril, Solhint, Manticore) and techniques to examine the code for issues such as incorrect function declarations, formal verification and avoided best practices. 

4. Manual Analysis: Line by line analysis of smart contracts This step involves testing the smart contract in a simulated environment to identify potential security risks and vulnerabilities that may not be visible through static analysis by writing unit tests. I use testing framework like Foundry to simulate different attack scenarios and identify any potential vulnerabilities. Checkout my [auditing checklist](Checklist.md).

5. Reporting: I provide a detailed report of my findings, including a description of the vulnerabilities and their severity, along with recommended remediation steps. The report also includes a summary of the audit findings and recommendations for improving the security of the smart contract. Checkout my [report template](ReportTemplate.md) for more details.

6. Remediation: Once the report is delivered, the development team can begin working on addressing the vulnerabilities identified in the audit. I can provide ongoing support and guidance throughout the remediation process.

7. Follow-up Audit: I recommend conducting a follow-up audit to ensure that the vulnerabilities have been addressed, and the smart contract is secure. This step ensures that any new issues that may have emerged during remediation are identified and resolved.

## Pricing

My smart contract security auditing service is designed to provide you with a flexible and cost-effective solution. I understand that budget constraints can be a concern, especially for startups and small businesses. That's why I offer a unique pricing model where you only pay for the findings.

Under this model, I will conduct a comprehensive analysis of your protocol, identifying any potential security risks and vulnerabilities. You will receive a detailed report of my findings, and you will only be charged for the actual findings, not the time spent on the audit.

This pricing model provides you with complete transparency and ensures that you get the most value for your investment. You can rest assured that you are only paying for the actual security risks and vulnerabilities found in your smart contract, rather than paying for a pre-determined package that may not be tailored to your specific needs.

## Questions before Audit

1. What is the clear scope (.sol files) of the security review ?
2. On what chains are the smart contracts going to be deployed?
3. Please list any known issues/acceptable risks that should not result in a valid finding.
4. Does the project have well written specifications & code documentation?
5. What is the code coverage percentage?
6. Are there any protocols that are similar to yours, which are they?
7. Is the admin/owner of the protocol/contracts TRUSTED or RESTRICTED?
8. Which ERC20, ERC721, ERC777 tokens do you expect will interact with the smart contracts?
9. Have you had any audits so far, are you planning to do other audits/security programs as well?

Based on the answers we can discuss the effort needed, the payment amount and the timeline.

## Security review result & fixes review

After the time agreed upon has passed, the project will receive the security review report. The project has 7 days to apply fixes on issues found. Each issues should be fixed in a separate commit that has a message pointing to the issue being fixed. Then, a single iteration of a "fixes review" will be executed by me, free of additional charges, to verify your fixes are correct and secure.
Important notes for the fixes review 
    - for any questions or clarifications on the vulnerabilities/recommendations in the report, you can reach out to me on the intended channel of communication
    - changes to be reviewed should not include anything else other than fixes for the reported issues, so no big refactorings, new features or architectural changes
    - in the case that fixes are too difficult to implement or more than one iteration of reviews is needed then this is a special case that can be discussed independently of this review


## Reports

Audit reports for my previous audits are in [here](reports), check them out.

My Previous public audits 

| Protocol | High Risk | Medium Risk | Low Risk | Gas & info | Link |
| -------- | --------- | ----------- | -------- | ---------- | ---- |
| Canto Identity Subprotocols | - | - | - | 1 | [Code4rena](https://code4rena.com/contests/2023-03-canto-identity-subprotocols-contest) |
| SPARKN protocol | - | - | 1 | - | [CodeHawks](https://www.codehawks.com/contests/cllcnja1h0001lc08z7w0orxx) |

## Auditing Resources

Are you interested in learning smart contract auditing? 

List of amazing resources are linked [here](resources).

## Disclaimer

It is important to note that while auditing can significantly reduce the risks of vulnerabilities in a smart contract, it can never guarantee the complete absence of vulnerabilities with 100% certainty. Auditing is a process of analyzing the code and identifying potential security risks, but it does not guarantee that all vulnerabilities have been discovered or that new ones will not emerge in the future.

Therefore, it is important to understand that the security of a smart contract is a continuous process and requires ongoing monitoring and updating. It is highly recommended to regularly review and update smart contracts, even after an audit, to ensure their continued security.

While I strive to provide the most accurate and reliable information possible, I make no claims or guarantees about the completeness or accuracy of the information provided. Any reliance on the information provided is solely at your own risk.

