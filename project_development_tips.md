# Smart Contract Project Development Standards

## Context

Smart Contracts are the bedrock piece of security for many important parts of the Flow blockchain, as well as for any project that is deployed to a blockchain.

They are also the most visible technical parts of any project, since users will be querying them for data, building other smart contracts that interact with them, and using them as learning materials and templates for future projects. Furthermore, when deployed they are publicly available code on the blockchain and often also in public Github repos.

Therefore, the process around designing, building, testing, documenting, and managing these projects needs to reflect the critical importance they hold in the ecosystem. Each project has a responsibility to set good examples for how to manage smart contract projects.

Some of these suggestions might seem somewhat unnecessary, but it is important to model what a project can do to manage its smart contracts the best so that hopefully all of the projects follow suit. It will also make all the Flow smart contracts that much safer and easier to use.

This also assumes standard software design best practices also apply. Indeed, many of these suggestions are more general software design best practices, but there may be others that are assumed but not included here.

### Implementing These Practices

This document serves as mostly an outline of best practices the projects should follow. Engineering leadership needs to figure out concrete steps for actually implementing them at their respective companies including detailed documents, education sessions, and workshops with all managers and Cadence developers.

## **Design Process**

- Ensure that there is a single person ultimately responsible for the project.
    - It is this person’s responsibility to lead design discussions with product managers and the community, write most of the code and tests, solicit reviews, make requested changes and make sure the project gets completed in a timely manner.
    - Even if the project is relatively easy, the owner should be someone who understands Cadence well and who keeps in touch with what is happening in the Cadence world. Examples:
        - Responsible project maintainers should contribute to discussions about important proposals (new cadence features, standard smart contracts, metadata, etc) and generally be aware about evolving best practices and anti-pattern understandings.
        - They should regularly re-evaluate the code of the project to see if it needs to be updated to conform to standards and new versions of Cadence.
        - The best projects should be active in the development of the protocol and language.
    - The owner should also understand how to sign transactions with the CLI to upgrade the smart contract, run admin transactions, deploy new contracts, etc. 
- The owner should identify a secondary owner who doesn’t hold any direct responsibility, but still has a clear understanding of the code and requirements so they can give good feedback, perform effective reviews, and make changes where needed. In case the owner is not available or leaves the project, this person can also take over easily so there is never a time when there is nobody who understands the smart contracts well.
- If there isn’t already an open source repo, the owner should create a public GitHub repo from [the open source template](https://github.com/onflow/open-source-template) and make sure all of this is set up with some initial documentation for what the repo is for before any code is written.
- The owner should create a design document that lays out the intended high level design and architecture of the smart contract and some basic user stories, as well as any questions that still need to be answered about it.
    - Diagrams should be made where applicable describing state machines, user flows, etc
    - This document should be shared in an issue in the open source repo where the contracts or features are being developed.
- Keys for the contract and/or admin accounts should be stored in a secure key store such as google KMS or something similar, and the owner should have access to these along with the secondary owner and some other engineering manager. Keys should never be in any file in the public repo.
- Project owners need to always keep [composability and extensibility](https://www.notion.so/Smart-Contract-Composability-be544f21a2e84596affad73952b21d56) in mind while designing, developing, and documenting their projects.
- Cadence best practices need to be kept in mind:
    - [https://developers.flow.com/cadence/design-pattern](https://developers.flow.com/cadence/design-patterns)s
    - [https://developers.flow.com/cadence/anti-patterns](https://developers.flow.com/cadence/anti-patterns)
    - [https://developers.flow.com/cadence/security-best-practices](https://developers.flow.com/cadence/security-best-practices)

## **Development Process**

- The same person who writes the code must also write the tests.
    - They have the clearest understanding of the code paths and edge cases.
- Development process should be iterative, if possible.
    - Develop MVP first, get reviews, and test thoroughly, then add additional features with tests.
    - Makes the review process easier.
- Comments and field/function descriptions need to be written at the same time (or even before) the code is written
    - Helps the developer and reviewers understand the work-in-progress code better, as well as the intentions of the design (for testing and reviewing)
- Functions should be commented with a
    - Description
    - Parameter descriptions
    - Return value descriptions
- Top Level comments and comments for types, fields, events, and functions should use `///` (three slashes) to be recognised by the [Cadence Documentation Generator](https://github.com/onflow/cadence-tools/tree/master/docgen)
    - regular comments within functions should only use two slashes (`//`)
- When looking for reviews, these requirements need to be followed (contracts and features that don’t have these are not ready for review and any reviewers should ask for them before doing the review):
    - Contract needs to be commented as described above
    - Include a high-level description of the contract or change in comments at the top of the file or function
    - Make a PR and make sure the PR description includes a summary of the contract, changes, and anything important to be aware of.

### **Testing**

- Tests should be **mandatory**, not optional, even if the contract is copied from somewhere else.
- There should be thorough emulator unit tests in the public repo.
- Every time there is a new Cadence version or emulator version, the dependencies of the repo should be updated to make sure the tests are all still passing.
- Tests should avoid being monolithic; Individual test cases should be set up for each part of the contract to test them in isolation.
    - There are some exceptions, like contracts that have to run through a state machine to test different cases.
- Positive and negative cases need to be tested.

### **Documentation**

- Detailed README.md
    - Explanation of the project itself with links to the app
    - Addresses on various networks
    - High-level technical description of the contracts with emphasis on important types and functionality
    - Architecture diagram (if applicable)
    - Include links to tutorials if they are external
- A high-level explanation of contracts at the top of each contract
- High-level descriptions of transactions and scripts at the top of each one

### **Tutorials**

Since all smart contracts are public, anyone can use them for their third-party application, interact with them through non-standard channels, or use them as a template for their own project.
Therefore, there should be clear tutorials for how to use and interact with the smart contracts so external developers can get up to speed as quickly as possible.

These can potentially be included in the README.md, but depending on the importance of the project, they could be their own posts or web pages.

Examples for tutorials:
- How to deploy and set up the contracts on the emulator and run automated tests.
- How to run common transactions.
- How to run scripts to access contract state on various networks.
- How to mint on testnet if applicable.

## **Deployment and Upgrade Process**

Smart contract upgrades are a big deal and need to be treated as such. It is important to have many eyes on the upgrades and more communication with the project team and community.

### Expectations for deployments to testnet or mainnet

- Communicate to all stake-holders
    - Share the code updates PR to managers and engineers on the project to try to get as many reviews as possible to make many people aware of the incoming changes.
    - Share the proposal with the community at least a week in advance (unless it is a critical bug fix)
        - In the #cadence channel in [the Flow discord server](https://discord.com/invite/J6fFnh2xx6).
        - On the Forum or project blog
    - Share the time of the deployment and the deployment transaction with branch/commit hash information to ensure the transaction itself is correct.
    - Coordinate deployment with managers to make sure it is done correctly and on time.

### **Community Engagement**

Once a contract is deployed, the work doesn’t stop there. As the developer of a public project on a public blockchain, the owners have an obligation to be helpful and responsive to the community so that they can encourage composability and third party interactions.

- Keep issues open in the repo.
- The owner should turn on email notifications for new issue creation in the repo.
- Respond to issues quickly and clean up unimportant ones.
- Maybe write a blog post about some part of the contracts every once in a while

If you have any feedback about these guidelines, please create an issue in the onflow/cadence-style-guide repo or make a PR updating the guidelines so we can start a discussion.