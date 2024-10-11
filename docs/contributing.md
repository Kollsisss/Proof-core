# Contributing to Proof Blockchain

Thank you for your interest in contributing to Proof Blockchain! This document provides guidelines on how you can get involved in the project and contribute to its development.

## Code of Conduct

This project and all its participants adhere to our [Code of Conduct](CODE_OF_CONDUCT.md). Please read and follow it in all your interactions with the project.

## Project Structure

Proof Blockchain is divided into three main repositories:

1. proof-core: The foundational layer (Layer 1) of the blockchain
2. proof-validators: The performance and scalability layer (Layer 2)
3. proof-nodes: The privacy and ultra-fast processing layer (Layer 3)

### proof-core Repository Structure

```
proof-core/
├── src/
│   ├── lib.rs
│   ├── config.rs
│   ├── errors.rs
│   ├── types.rs
│   ├── block/
│   │   ├── mod.rs
│   │   ├── header.rs
│   │   └── body.rs
│   ├── chain/
│   │   ├── mod.rs
│   │   ├── state.rs
│   │   └── validator_set.rs
│   ├── consensus/
│   │   ├── mod.rs
│   │   └── dpos.rs
│   ├── crypto/
│   │   ├── mod.rs
│   │   ├── hash.rs
│   │   ├── merkle.rs
│   │   └── signature.rs
│   ├── network/
│   │   ├── mod.rs
│   │   ├── p2p.rs
│   │   └── sync.rs
│   ├── storage/
│   │   ├── mod.rs
│   │   ├── db.rs
│   │   └── trie.rs
│   ├── transaction/
│   │   ├── mod.rs
│   │   ├── pool.rs
│   │   └── validation.rs
│   ├── utils/
│   │   ├── mod.rs
│   │   └── serialization.rs
│   └── zz_protocol/
│       ├── mod.rs
│       ├── block_production.rs
│       └── finality.rs
├── benches/
│   └── benchmarks.rs
├── examples/
│   └── simple_transaction.rs
├── tests/
│   ├── block_tests.rs
│   ├── consensus_tests.rs
│   └── network_tests.rs
├── Cargo.toml
├── Cargo.lock
├── README.md
└── LICENSE
```

### proof-validators Repository Structure

```
proof-validators/
├── src/
│   ├── main.rs
│   ├── config.rs
│   ├── errors.rs
│   ├── types.rs
│   ├── validator/
│   │   ├── mod.rs
│   │   ├── stake.rs
│   │   └── rewards.rs
│   ├── xx_protocol/
│   │   ├── mod.rs
│   │   ├── execution.rs
│   │   ├── sharding.rs
│   │   └── cross_shard.rs
│   ├── yy_protocol/
│   │   ├── mod.rs
│   │   ├── altcoin_integration.rs
│   │   ├── bridge.rs
│   │   └── liquidity_pools.rs
│   ├── smart_contracts/
│   │   ├── mod.rs
│   │   ├── vm.rs
│   │   └── execution.rs
│   ├── consensus/
│   │   ├── mod.rs
│   │   └── pbft.rs
│   ├── network/
│   │   ├── mod.rs
│   │   └── validator_communication.rs
│   └── storage/
│       ├── mod.rs
│       └── state_storage.rs
├── benches/
│   └── validator_benchmarks.rs
├── examples/
│   └── run_validator.rs
├── tests/
│   ├── xx_protocol_tests.rs
│   ├── yy_protocol_tests.rs
│   └── smart_contract_tests.rs
├── Cargo.toml
├── Cargo.lock
├── README.md
└── LICENSE
```

### proof-nodes Repository Structure

```
proof-nodes/
├── src/
│   ├── main.rs
│   ├── config.rs
│   ├── errors.rs
│   ├── types.rs
│   ├── node/
│   │   ├── mod.rs
│   │   ├── full_node.rs
│   │   └── light_node.rs
│   ├── zk_rollups/
│   │   ├── mod.rs
│   │   ├── prover.rs
│   │   ├── verifier.rs
│   │   └── batch_processor.rs
│   ├── privacy/
│   │   ├── mod.rs
│   │   └── zero_knowledge.rs
│   ├── network/
│   │   ├── mod.rs
│   │   ├── p2p.rs
│   │   └── sync.rs
│   ├── api/
│   │   ├── mod.rs
│   │   ├── rpc.rs
│   │   └── rest.rs
│   ├── storage/
│   │   ├── mod.rs
│   │   └── offchain_storage.rs
│   └── utils/
│       ├── mod.rs
│       └── crypto_utils.rs
├── benches/
│   └── zk_rollup_benchmarks.rs
├── examples/
│   └── run_zk_rollup_node.rs
├── tests/
│   ├── zk_rollup_tests.rs
│   ├── privacy_tests.rs
│   └── api_tests.rs
├── Cargo.toml
├── Cargo.lock
├── README.md
└── LICENSE
```

## How to Contribute

1. Fork the relevant repository (proof-core, proof-validators, or proof-nodes)
2. Clone your fork: `git clone https://github.com/your-username/[repository-name].git`
3. Create a new branch for your feature: `git checkout -b feature/amazing-feature`
4. Make your changes
5. Commit your changes: `git commit -m 'Add some amazing feature'`
6. Push to the branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

## Reporting Bugs

If you find a bug, please open an issue in the relevant GitHub repository. Make sure to include:

* A clear title and description of the problem
* Steps to reproduce the issue
* Expected behavior
* Actual behavior
* Version of Proof Blockchain you are using
* Any additional information that may be helpful

## Suggesting Improvements

If you have an idea for a new feature or improvement, please:

1. First, check if a similar suggestion already exists in issues or pull requests
2. Open a new issue describing your proposal
3. Discuss the idea with the community and the Proof Blockchain team
4. If you receive positive feedback, you can start working on the implementation

## Coding Style

To maintain consistency in the codebase, please follow these guidelines:

### General Rules
* Use 4 spaces for indentation (no tabs)
* Maximum line length: 100 characters
* Use meaningful names for variables and functions
* Comment on complex logic, but avoid unnecessary comments

### Rust-Specific Rules
* Follow the official [Rust Style Guide](https://rust-lang.github.io/api-guidelines/)
* Use `rustfmt` for code formatting
* Run `clippy` for static analysis

## Code Review Process

1. All changes must go through the code review process.
2. At least one member of the core team must approve the changes.
3. All automated tests must pass successfully.
4. Code that decreases test coverage will not be accepted.

## Setting Up the Development Environment

1. Install Rust (version 1.55.0 or newer).
2. Clone the repository you want to work on:
   ```bash
   git clone https://github.com/proof-blockchain/[repository-name].git
   cd [repository-name]
   ```
3. Install the necessary dependencies:
   ```bash
   cargo build
   ```
4. Set up pre-commit hooks:
   ```bash
   pre-commit install
   ```

## Testing

* Run unit tests:
  ```bash
  cargo test
  ```
* For integration tests:
  ```bash
  cargo test --test '*' --features "integration-tests"
  ```
* Ensure that you add tests for every new feature or bug fix.

## Documentation

* Keep the README files up to date.
* Document public APIs with comments in the code.
* Use `///` for documentation comments, following Rustdoc standards.

## Specific Guidelines for Each Repository

### proof-core
* Focus on core blockchain functionality and consensus mechanisms.
* Ensure high security standards in all implemented features.
* Thoroughly test all cryptographic implementations.

### proof-validators
* Implement and optimize validator logic and reward mechanisms.
* Focus on scalability and efficient cross-shard communication.
* Ensure proper integration with Layer 1 (proof-core) functionality.

### proof-nodes
* Implement ZK-rollup functionality and privacy features.
* Optimize for high throughput and low latency.
* Ensure secure off-chain data management.

## Communication

* Use [GitHub Issues](https://github.com/proof-blockchain/[repository-name]/issues) for reporting bugs and feature requests.
* Join our [Discord server](https://discord.gg/proofblockchain) for discussions.
* Follow our [blog](https://blog.proofblockchain.com) for important announcements and updates.

Thank you again for your interest in contributing to Proof Blockchain. Your efforts help make this project better for everyone!