# Decentralized Bitcoin Cloud Storage Smart Contract

## Overview
The **Decentralized Cloud Storage** smart contract enables users to securely store, update, delete, and transfer file ownership on a blockchain. It also supports permission-based file access control. This contract is designed to be trustless and transparent, ensuring users have full control over their files and who can access them.

## Features
- **Upload Files**: Users can upload files with a name and size.
- **Update Files**: Owners can modify file names and sizes.
- **Delete Files**: Owners can remove files from storage.
- **Transfer Ownership**: File ownership can be transferred to another user.
- **Permission Management**: Owners can grant or revoke file access to other users.
- **Read-Only Queries**: Users can fetch file metadata and total uploaded files.

## Contract Constants
- `contract-owner`: The deployer of the contract.
- `err-owner-only (u100)`: Error when a non-owner attempts restricted actions.
- `err-not-found (u101)`: Error when a requested file does not exist.
- `err-already-exists (u102)`: Error when trying to upload a duplicate file.
- `err-invalid-name (u103)`: Error when the file name is invalid.
- `err-invalid-size (u104)`: Error when the file size is invalid.
- `err-unauthorized (u105)`: Error when a user tries to perform an unauthorized action.
- `err-invalid-recipient (u106)`: Error when the recipient of a file transfer is invalid.

## Data Structures
### Variables
- `total-files (uint)`: Stores the total count of uploaded files.

### Maps
- `files`: Stores metadata of uploaded files, indexed by `file-id`.
- `file-permissions`: Stores file access permissions, indexed by `file-id` and `user`.

## Functions
### Public Functions
#### `upload-file (name (string-ascii 64)) (size uint) -> (response uint uint)`
Uploads a file with the given name and size.

#### `update-file (file-id uint) (new-name (string-ascii 64)) (new-size uint) -> (response bool uint)`
Allows file owners to update file metadata.

#### `delete-file (file-id uint) -> (response bool uint)`
Deletes a file if the caller is the owner.

#### `transfer-file-ownership (file-id uint) (new-owner principal) -> (response bool uint)`
Transfers file ownership to another user.

#### `grant-permission (file-id uint) (permission bool) (recipient principal) -> (response bool uint)`
Allows file owners to grant read access to other users.

#### `revoke-permission (file-id uint) (user principal) -> (response bool uint)`
Allows file owners to revoke file access from other users.

### Read-Only Functions
#### `get-total-files () -> (response uint uint)`
Returns the total number of uploaded files.

#### `get-file-info (file-id uint) -> (response (tuple (owner principal) (name (string-ascii 64)) (size uint) (created-at uint)) uint)`
Fetches metadata of a specific file.

## Usage
1. Deploy the contract on the blockchain.
2. Users can upload files using `upload-file`.
3. Owners can manage file properties using `update-file`, `delete-file`, and `transfer-file-ownership`.
4. Owners can control access using `grant-permission` and `revoke-permission`.
5. Users can retrieve file metadata using `get-file-info`.

## Error Handling
All functions return `ok` on success and appropriate error codes on failure.

## Security Considerations
- Only owners can update, delete, or transfer files.
- Permissions must be explicitly granted by owners.
- File metadata is stored immutably on-chain.

## License
This project is released under the MIT License.

