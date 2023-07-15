# Cadence Style Guide
## Table of contents
1. [Indentation](#indentation)
1. [Line length](#line-length)
1. [Comments](#comments)
1. [Whitespace between code lines](#whitespace-between-code-lines)
1. [Declaring variables and constants](#whitespace-between-code-lines)
1. [Bracket spaces](#bracket-spaces)
1. [Panic messages](#panic-messages)
1. [Naming and capitalization](#naming-and-capitalization)
## Indentation
Use 4 spaces per indentation level.
Prefer spaces over tabs as indentation method, mixing them should be avoided.
## Line length
A line length of 80 characters is recommended for Cadence. This could be particularly challenging when writing capability-related lines, for instance:
```cadence
letResourceRef = account.getCapability(ContractName.SomePathName).borrow<&SomeResource{ContractName.InterfaceName}>()
```
This generic line of code that can be found in many transactions that need to borrow a reference to a certain object from a capability is 118 characters long by its own without any indentation. Keeping this line readable should be an objective of any Cadence developer. There are some simple patterns that could be observed in order to accomplish this:
+ Prefer to always break the line before the `borrow` call.
```cadence
letResourceRef = account.getCapability(ContractName.SomePathName)
                  .borrow<&SomeResource{ContractName.InterfaceName}>()
```
+ If indentation or a long path name makes the "getCapability" line go further than 80 characters an additional line break can be included
```cadence
letResourceRef = account
                  .getCapability(ContractName.SomeAbsurdlyLongForSomeReasonPathName)
                  .borrow<&SomeResource{ContractName.InterfaceName}>()
```
Always keep those concatenated function calls indented from the object they are being called from.
## Comments
Comments are a vital part of smart contracts, allowing users to easily understand what they are getting involved with. 
### High level documentation at the begining of files (contracts, transactions and scripts)
Top Level comments and comments for types, fields, events, and functions should use `///` (three slashes) because [the cadence docs generating tool](https://github.com/onflow/cadence/tree/master/tools/docgen) picks up three slash comments to auto-generate docs.
### Commenting functions
## Whitespace between code lines
## Declaring variables and constants
## Bracket spaces
## Panic messages
## Naming and capitalization
### Contracts
Contract and contract interfaces names should always follow PascalCase, for instance:
```cadence
pub contract ExampleToken
```
### Fields
```cadence
pub var totalSupply
```
```cadence
pub var VaultStoragePath
```
// Different rule for regular fields than for path fields?
### Functions
Function names should always follow camelCase, for instance:
```cadence
pub fun mintTokens
```
### Paths
