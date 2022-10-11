# Smart Contract Project Development Standards

## Context

Smart Contracts are the bedrock piece of security for many important parts
of the Flow blockchain, as well as for any project that is deployed to a blockchain.

They are also the most visible technical parts of any project,
since users will be querying them for data, building other smart contracts that interact with them,
and using them as learning materials and templates for future projects.
Furthermore, when deployed they are publicly available code on the blockchain
and often also in public Github repos.

Therefore, the process around designing, building, testing, documenting,
and managing these projects needs to reflect the critical importance they hold in the ecosystem.
Each project has a responsibility to manage their project clearly and professionally.
If they do so, they will be able to build better smart contracts, avoid potential bugs,
support user and third-party adoption of their projects, and increase their chances of success
by being a model for good software design. Additionally, the more projects that adopt
good software design and management standards normalizes this behavior,
encouraging other projects in the ecosystem to do the same which creates a healthier
and more vibrant community.

Some of these suggestions might seem somewhat unnecessary,
but it is important to model what a project can do to manage its smart contracts the best
so that hopefully all of the projects follow suit.
It will also make all the Flow smart contracts that much safer and easier to use.

This also assumes standard software design best practices also apply.
Indeed, many of these suggestions are more general software design best practices,
but there may be others that are assumed but not included here.

### Implementing These Practices

This document serves as mostly an outline of best practices the projects should follow.
As with all best practices, teams will choose which applies to them and their work process,
however, we recommend that teams explicitly define a minimum acceptable set of standards
for themselves along with the mechanisms to ensure they are being observed.

Some teams may also have their own set of development standards that acheive a similar goal
to these. These recommendations are not meant to be the only paths to success,
so if a team disagrees with some of these and wants to do things their own way,
they are welcome to pursue that. This document just shows some generic suggestions
for teams who might not know how they want to manage their project.

## Design Process

Smart contracts usually manage a lot of value, have many users, and are difficult to upgrade
for a variety of reasons. Therefore, it is important to have a clearly defined design
process for the smart contracts before much code is written so that the team
can set themselves up for success.

Here are some recommendations for how projects can organize the foundations of their projects.

### Projects should have a single person ultimately responsible for the smart contract

This person should be someone who understands Cadence well and has written Cadence smart contracts
before. Production-level smart contracts are not the place for beginners to get their start.

It should be this person’s responsibility to lead design discussions
with product managers and the community, write most of the code and tests,
solicit reviews, make requested changes and make sure the project gets completed in a timely manner.

The owner should also understand how to sign transactions with the CLI
to upgrade the smart contract, run admin transactions, deploy new contracts, etc.
If something goes wrong or needs to be handled with a transaction, it is important that the owner
know how to run transaction and scripts safely to address the issues.

The owner should identify a secondary owner who doesn’t hold any direct responsibility,
but still has a clear understanding of the code and requirements so they can give good feedback,
perform effective reviews, and make changes where needed.
In case the owner is not available or leaves the project,
this person can also take over easily so there is never a time
when there is nobody who understands the smart contracts well.

### Projects should maintain a well-organized open source Repo for their smart contracts

If there isn’t already an open source repo, the owner should create a public GitHub repo
from [the Flow open source template](https://github.com/onflow/open-source-template)
and make sure all of this is set up with some initial documentation for what the repo is for
before any code is written. External developers and users should have an easily accessible home page
to go to to understand any given project.

The repo should also have some sort of high-level design document that lays out
the intended design and architecture of the smart contract and some basic user stories,
as well as any questions that still need to be answered about it.
    - Where applicable, diagrams should be made describing state machines, user flows, etc.
    - This document should be shared in an issue in the open source repo
    where the contracts or features are being developed,
    then later moved to the README or another important docs page.

## Development Process Recommendations

### The Development process should be iterative, if possible

The project should develop an MVP first, get reviews, and test thoroughly,
then add additional features with tests. This ensures that the core features are designed
thoughtfully and makes the review process easier because they can focus on each feature
one at a time instead of being overwhelmed by a huge block of code.

### Comments and field/function descriptions should be standardized and written early

Comments should be written at the same time (or even before) the code is written.
This helps the developer and reviewers understand the work-in-progress code better,
as well as the intentions of the design (for testing and reviewing).
Functions should be commented with a
    - Description
    - Parameter descriptions
    - Return value descriptions


Top Level comments and comments for types, fields, events,
and functions should use `///` (three slashes) to be recognised by the
[Cadence Documentation Generator](https://github.com/onflow/cadence-tools/tree/master/docgen).
Regular comments within functions should only use two slashes (`//`)

## Testing Recommendations


The same person who writes the code should also write the tests.
They have the clearest understanding of the code paths and edge cases.


Tests should be **mandatory**, not optional, even if the contract is copied from somewhere else.
There should be thorough emulator unit tests in the public repo.


Every time there is a new Cadence version or emulator version,
the dependencies of the repo should be updated to make sure the tests are all still passing.


Tests should avoid being monolithic;
Individual test cases should be set up for each part of the contract to test them in isolation. 
There are some exceptions, like contracts that have to run through a state machine
to test different cases. Positive and negative cases need to be tested.

Integration tests should also be written to ensure that your app and/or backend can interact
properly with the smart contracts.

## Managing Project Keys and Deployments

Smart contract keys and deployments are very important and need to be treated as such.

### Private Keys should be stored securely

Private Keys for the contract and/or admin accounts should not be kept in plain text format anywhere.
Projects should determine a secure solution that works best for them to store their private keys.
We recommend storing them in a secure key store such as google KMS or something similar.

### Deployments to Testnet or Mainnet should be handled transparently

When deploying or upgrading a contract, it is important to have many eyes on the upgrades
and clear communication with the project team and community. This builds trust with the community,
allows the opportunity to catch issues with upgrades before they happen, and provides more time
and context for community members to react to new features and changes.
Here are a few suggestions for how to manage a deployment or upgrade.

- Communicate to all stake-holders well in advance
    - Share the proposal with the community at least a week in advance (unless it is a critical bug fix)
        - Examples of places to share are your project's chat, forum, blog, email list, etc.
        - This will allow the community and other stakeholders to have plenty of time
        to view the upcoming changes and provide feedback if neccessary.
    - Share the time of the deployment and the deployment transaction with branch/commit hash information to ensure the transaction itself is correct.
    - Coordinate deployment with stakeholders to make sure it is done correctly and on time.

## Responsibilities to the Community

### Project should have thorough Documentation

Each project should have a Detailed README.md with these sections:
    - Explanation of the project itself with links to the app
    - Addresses on various networks
    - High-level technical description of the contracts with emphasis on important types and functionality
    - Architecture diagram (if applicable)
    - Include links to tutorials if they are external

Additionally, each contract, transaction, and script should have high-level descriptions
at the top of their files. This way, anyone in the community can easily 
come in and understand what each one is doing without having to parse confusing code.

### Projects should Engage with and respond to their own Community

Once a contract is deployed, the work doesn’t stop there. As the developer of a public project on a public blockchain, the owners have an obligation to be helpful and responsive to the community so that they can encourage composability and third party interactions.

- Keep issues open in the repo.
- The owner should turn on email notifications for new issue creation in the repo.
- Respond to issues quickly and clean up unimportant ones.
- Maybe write a blog post about some part of the contracts every once in a while.

### Projects should contribute to the greater Flow and Cadence Community

Responsible project maintainers should contribute to discussions
about important proposals (new cadence features, standard smart contracts, metadata, etc)
and generally be aware about evolving best practices and anti-pattern understandings.
Projects who contribute to these discussions are able to influence them to ensure
that the language/protocol changes are favorable to them
and the rest of the app developers in the ecosystem.
It also helps the owner to promote the project and themselves.

Owners should also regularly re-evaluate the code of their project to see if it needs to be updated 
to conform to new standards and new versions of Cadence.
This will help them identify potential problems with their smart contracts ahead of time
and be able to stay on the cutting edge of smart contract development.

Resources for Best Practices:

- [https://developers.flow.com/cadence/design-pattern](https://developers.flow.com/cadence/design-patterns)s
- [https://developers.flow.com/cadence/anti-patterns](https://developers.flow.com/cadence/anti-patterns)
- [https://developers.flow.com/cadence/security-best-practices](https://developers.flow.com/cadence/security-best-practices)

Composability and extensibility should also be priorities while designing, developing,
and documenting their projects. (Documentation for these topics coming soon)



If you have any feedback about these guidelines, please create an issue in the onflow/cadence-style-guide repo or make a PR updating the guidelines so we can start a discussion.