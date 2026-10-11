# Project 24: Blockchain-Based Voting System
## Introduction

Electronic voting systems must provide integrity, transparency, and voter privacy. A blockchain-based approach is useful because it stores data in append-only blocks linked by hashes, makes tampering visible, and allows multiple nodes to validate the same ledger state.

This project implements a distributed voting application with a web frontend, one leader node, two validator nodes, and Merkle proof verification. The selected project variant is **Variant C**, where voters can verify that their vote was included in the blockchain without revealing their identity.

The system is relevant because it demonstrates how blockchain concepts such as immutable ledgers, distributed validation, and Merkle trees can be applied to a voting problem in a practical academic project.

## Methods

### System Overview

The system contains four services:

- `frontend` serves the voting and verification interface
- `leader` accepts votes, creates blocks, and coordinates validation
- `validator1` validates proposed blocks and stores a replicated ledger
- `validator2` validates proposed blocks and stores a replicated ledger

The backend is implemented in Python using `FastAPI`. Each node stores data in `SQLite`. The frontend is a static HTML/CSS/JavaScript application served by `Nginx`.

### Architecture

```text
Client Browser
    |
    v
Frontend (Nginx, static UI)
    |
    v
Leader Node (FastAPI + SQLite)
    |  \
    |   \__ sends proposed block for validation
    |    
    +------> Validator 1 (FastAPI + SQLite)
    |
    +------> Validator 2 (FastAPI + SQLite)

After approval:
- leader commits the block
- validators store replicated copies
- receipt with Merkle proof becomes available to the voter
```

### Voting Workflow

1. A user opens the frontend and selects a candidate.
2. The user enters a unique voter ID and a password.
3. The frontend sends the vote to the leader node.
4. The leader hashes the voter ID using a salt and generates a vote hash.
5. The leader checks whether the voter has already voted.
6. If valid, the vote is stored in `pending_votes`.
7. Every 10 seconds, the leader builds a new block from all pending votes.
8. The block includes a Merkle root calculated from vote hashes.
9. The leader sends the block to both validator nodes.
10. Validators verify the block structure, previous hash, Merkle root, and duplicate-voter constraints.
11. If approval is sufficient, the block is committed and replicated.
12. A receipt with `vote_hash`, `block_index`, and `merkle_proof` is stored for the voter.

### Data Model

#### Block

Each block stores:

- `index`
- `timestamp`
- `previous_hash`
- `merkle_root`
- `block_hash`
- `proposer_node`
- `vote_count`

#### Vote Record

Each committed vote stores:

- `vote_hash`
- `voter_id_hash`
- `candidate_id`
- `timestamp`
- `block_index`

#### Receipt

Each receipt stores:

- `vote_hash`
- `block_index`
- `merkle_root`
- `merkle_proof`
- `candidate_id`
- `timestamp`

### Security and Validation Logic

The raw voter ID is not stored in the ledger. Instead, the application stores:

`voter_id_hash = SHA-256(salt + voter_id)`

This improves privacy and supports duplicate-vote prevention without directly exposing the original voter ID.

Double voting is prevented in two stages:

- the leader checks whether `voter_id_hash` already exists in `pending_votes` or committed `votes`
- validator nodes repeat duplicate-voter checks before approving a proposed block

Each block is linked to the previous block using `previous_hash`, which makes ledger tampering visible. The Merkle root is stored in the block so that each voter can later verify vote inclusion using a Merkle proof.

### Tools and Configuration

- `Python`
- `FastAPI`
- `SQLite`
- `Pydantic`
- `Docker`
- `Docker Compose`
- `Nginx`

Important configuration from `docker-compose.yml`:

- leader runs on host port `8001`
- validator1 runs on host port `8002`
- validator2 runs on host port `8003`
- frontend runs on host port `8080`
- block interval is `10` seconds

## Results

### Validation Checklist Mapping

#### 1. Log all vote submissions with time, hash, and unique voter ID or signature

Implemented by storing:

- `timestamp`
- `vote_hash`
- `voter_id_hash`

Both pending and committed votes are persisted in SQLite.

#### 2. Validate that each vote appears exactly once in the final ledger

Implemented by:

- duplicate checking in the leader before accepting a vote
- repeated duplicate checking in validators during block approval
- unique constraints in the database on `voter_id_hash`

#### 3. Demonstrate a verification method for a voter to prove their vote was counted

Implemented by:

- generating a receipt after block commit
- storing `vote_hash`, `block_index`, and `merkle_proof`
- verifying the receipt against the block Merkle root

#### 4. Simulate multiple nodes accepting and verifying blocks and test the consensus process

Implemented by:

- one leader node building blocks
- two validator nodes approving blocks
- replicated block storage on leader and validators

### Observed Execution Results

A scripted execution was performed from the repository code to collect concrete evidence.

Test scenario:

- 3 valid votes were submitted
- 1 duplicate vote attempt was made
- 1 block was created
- both validators approved the block
- the block was committed and replicated
- one receipt was verified successfully

Observed outcomes:

- duplicate vote attempt returned: `This voter has already voted.`
- validator approvals: `2`
- committed blocks in leader ledger: `1`
- committed votes in final ledger: `3`
- Merkle verification result: `true`

Vote totals in the demonstration:

| Candidate | Votes |
| --- | ---: |
| Milo | 1 |
| Luna | 1 |
| Oscar | 1 |

Example committed block data:

- `block_hash`: `09d261d1637a4407b742ece2b12429526a445f8f7ba41b06ab3d6a8b362fcfa4`
- `merkle_root`: `aa662d2b7898b729ab9a5cbf26c7d0359e0a6c1324fee363110ce8068a876ead`

Example verification receipt:

- `vote_hash`: `6a388254f6cc412f94f0af64db283f44f1d575fab5fb2076df64d66d2efb35e3`
- `block_index`: `1`
- proof path contains sibling hashes used to recompute the Merkle root

### Evidence of Replication

The recorded execution showed that:

- the leader ledger contained the committed block
- `validator1` stored the same block
- `validator2` stored the same block

This demonstrates replicated ledger state across nodes after approval.

## Discussion

The project satisfies the main academic requirements. It records vote submissions, prevents double voting, creates an immutable hash-linked ledger, and allows anonymous vote inclusion verification through Merkle proofs.

The system is also practical for demonstration purposes because:

- it has a clear multi-node structure
- it includes a usable web interface
- it exposes endpoints for viewing the chain, results, and receipts
- it is easy to deploy with Docker Compose

There are still limitations:

- voter identity is simulated by a user-entered ID and password, not by a government or institutional identity system
- the database is SQLite, which is acceptable for a course project but limited for large-scale use
- the architecture still depends on a leader node, so it is not a fully decentralized blockchain
- the system uses a simplified proof-of-authority style flow rather than a full production consensus protocol

One important implementation note is that the code behaves like a leader-based approval model where validator confirmations are required for commit. This is suitable for a course project, but a stricter production design would define consensus thresholds and failure handling more formally.

Possible improvements:

- integrate digital signatures
- add stronger voter authentication
- improve fault tolerance and recovery logic
- add automated consensus and verification tests
- measure performance under higher vote volume

## Conclusion

This project demonstrates a complete blockchain-based voting workflow for an academic setting. Votes are submitted through a web interface, validated by distributed nodes, committed into hash-linked blocks, and verified later using Merkle proofs. The result is a coherent example of how blockchain principles can be used to support integrity, transparency, and privacy in a voting application.
