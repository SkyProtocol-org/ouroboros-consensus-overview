# Overview

Cardano's Ouroboros is a family of proof-of-stake (PoS) consensus protocols that underpin the Cardano blockchain. It is designed to be secure, scalable, and sustainable, providing a robust foundation for decentralized applications. Ouroboros is notable for its rigorous security proofs and its ability to support a global network of nodes.

## Key Features of Ouroboros

1. Proof-of-Stake Mechanism: Ouroboros uses a PoS mechanism where the probability of being selected to add a new block is proportional to the stake a node holds in the network.
2. Epochs and Slots: The blockchain is divided into epochs, which are further divided into slots. Each slot has a designated slot leader responsible for adding a block to the chain.
3. Security: Ouroboros is the first PoS protocol with a mathematically proven level of security comparable to Bitcoin's proof-of-work (PoW) protocol.
4. Energy Efficiency: By eliminating the need for energy-intensive PoW computations, Ouroboros is more energy-efficient and environmentally friendly.
5. Decentralization: The protocol is designed to support a large number of nodes, promoting decentralization and resilience against attacks.

## Components of Ouroboros Consensus

### 1. Block Forging

The [BlockForging](https://github.com/IntersectMBO/ouroboros-consensus/blob/358305b09f8fa1a85f076b20a51b4af03e827071/ouroboros-consensus/src/ouroboros-consensus/Ouroboros/Consensus/Block/Forging.hs#L80) module is responsible for the creation of new blocks. It includes logic for determining whether a node can forge a block in a given slot.

```haskell
data BlockForging m blk = BlockForging {
    forgeLabel :: Text,
    canBeLeader :: CanBeLeader (BlockProtocol blk),
    ...
}
```

### 2. Chain Selection

The chain selection logic ensures that nodes agree on the longest valid chain. This is crucial for maintaining consensus across the network.

[SupportsProtocol](https://github.com/IntersectMBO/ouroboros-consensus/blob/358305b09f8fa1a85f076b20a51b4af03e827071/ouroboros-consensus/src/ouroboros-consensus/Ouroboros/Consensus/Block/SupportsProtocol.hs#L24)

```haskell
class BlockSupportsProtocol blk where
    selectView :: BlockConfig blk -> Header blk -> SelectView (BlockProtocol blk)
```

### 3. Blockchain Time

The [BlockchainTime](https://github.com/IntersectMBO/ouroboros-consensus/blob/358305b09f8fa1a85f076b20a51b4af03e827071/ouroboros-consensus/src/ouroboros-consensus/Ouroboros/Consensus/BlockchainTime/API.hs#L28) module provides an abstraction over the system clock, allowing the protocol to operate in a time-aware manner. This is essential for slot-based operations.

```haskell
data BlockchainTime m = BlockchainTime {
    getCurrentSlot :: STM m SlotNo
}
```

### 4. Sanity Checks

Sanity checks are performed to ensure that the node's configuration is consistent and does not lead to unexpected behavior.

```haskell
sanityCheckConfig :: BlockSupportsSanityCheck blk => TopLevelConfig blk -> [SanityCheckIssue]
```
