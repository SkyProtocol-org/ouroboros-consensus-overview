# Build and Test Guide

## Clone Repository

Clone `ouroboros-consensus`:

```bash
git clone https://github.com/IntersectMBO/ouroboros-consensus.git
cd ouroboros-consensus
git checkout 358305b
```

## Setup Environment

Install Haskell:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh
```

Update `cabal`:

```bash
cabal update
```

## Build

Build `ouroboros-consensus`:

```bash
cabal build all
```
