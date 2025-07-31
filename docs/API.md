# Pump.fun Smart Contract API Documentation

## Overview

The Pump.fun Smart Contract provides a comprehensive API for managing virtual liquidity pools, creating Raydium pools, and integrating with various DeFi protocols on the Solana blockchain.

## Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
- [Core API](#core-api)
- [Advanced Features](#advanced-features)
- [Error Handling](#error-handling)
- [Examples](#examples)
- [Best Practices](#best-practices)

## Installation

### Prerequisites

```bash
npm install @coral-xyz/anchor @solana/web3.js @solana/spl-token
```

### Setup

```typescript
import { Connection, PublicKey } from '@solana/web3.js';
import { Program, AnchorProvider } from '@coral-xyz/anchor';

// Initialize connection
const connection = new Connection('https://api.devnet.solana.com');
const provider = new AnchorProvider(connection, wallet, {});
const program = new Program(IDL, PROGRAM_ID, provider);
```

## Quick Start

### Basic LP Management

```typescript
// Add virtual liquidity
const addLpTx = await program.methods
  .addVirtualLp(new BN(1000000), tokenMint)
  .accounts({
    user: wallet.publicKey,
    pool: poolAddress,
    tokenAccount: tokenAccount,
  })
  .rpc();

// Remove virtual liquidity
const removeLpTx = await program.methods
  .removeVirtualLp(new BN(500000), tokenMint)
  .accounts({
    user: wallet.publicKey,
    pool: poolAddress,
    tokenAccount: tokenAccount,
  })
  .rpc();
```

## Core API

### Virtual LP Management

#### `addVirtualLp(amount: BN, tokenMint: PublicKey)`

Adds virtual liquidity to a pool.

**Parameters:**
- `amount`: Amount of tokens to add (BN)
- `tokenMint`: Token mint address (PublicKey)

**Returns:** Transaction signature (string)

**Example:**
```typescript
const tx = await program.methods
  .addVirtualLp(new BN(1000000), tokenMint)
  .accounts({
    user: wallet.publicKey,
    pool: poolAddress,
    tokenAccount: tokenAccount,
  })
  .rpc();
```

#### `removeVirtualLp(amount: BN, tokenMint: PublicKey)`

Removes virtual liquidity from a pool.

**Parameters:**
- `amount`: Amount of tokens to remove (BN)
- `tokenMint`: Token mint address (PublicKey)

**Returns:** Transaction signature (string)

### Raydium Pool Creation

#### `createRaydiumPool(tokenAMint: PublicKey, tokenBMint: PublicKey, initialLiquidity: BN)`

Creates a new Raydium pool with specified tokens.

**Parameters:**
- `tokenAMint`: First token mint address (PublicKey)
- `tokenBMint`: Second token mint address (PublicKey)
- `initialLiquidity`: Initial liquidity amount (BN)

**Returns:** Transaction signature (string)

**Example:**
```typescript
const tx = await program.methods
  .createRaydiumPool(tokenAMint, tokenBMint, new BN(1000000))
  .accounts({
    authority: wallet.publicKey,
    raydiumProgram: raydiumProgramId,
    pool: poolAddress,
  })
  .rpc();
```

### Pool Management

#### `updatePoolFees(newFeeRate: BN)`

Updates the pool fee configuration.

**Parameters:**
- `newFeeRate`: New fee rate in basis points (BN)

**Returns:** Transaction signature (string)

#### `getPoolInfo(poolAddress: PublicKey)`

Retrieves pool information.

**Parameters:**
- `poolAddress`: Pool address (PublicKey)

**Returns:** Pool information object

## Advanced Features

### Meteora Integration

```typescript
// Integrate with Meteora DEX
const meteoraTx = await program.methods
  .integrateMeteora(tokenMint, amount)
  .accounts({
    user: wallet.publicKey,
    meteoraProgram: meteoraProgramId,
  })
  .rpc();
```

### EVM Compatibility

```typescript
// Cross-chain functionality
const evmTx = await program.methods
  .bridgeToEVM(tokenMint, amount, targetChain)
  .accounts({
    user: wallet.publicKey,
    bridgeProgram: bridgeProgramId,
  })
  .rpc();
```

## Error Handling

### Custom Error Types

```typescript
export enum PumpError {
  InsufficientLiquidity = "Insufficient liquidity in pool",
  InvalidTokenMint = "Invalid token mint address",
  PoolNotFound = "Pool not found",
  Unauthorized = "Unauthorized operation",
  InvalidFeeRate = "Invalid fee rate",
}
```

### Error Handling Example

```typescript
try {
  const tx = await program.methods
    .addVirtualLp(amount, tokenMint)
    .accounts({
      user: wallet.publicKey,
      pool: poolAddress,
    })
    .rpc();
  console.log('Transaction successful:', tx);
} catch (error) {
  if (error.message.includes('Insufficient liquidity')) {
    console.error('Not enough liquidity in pool');
  } else if (error.message.includes('Invalid token mint')) {
    console.error('Invalid token mint address');
  } else {
    console.error('Transaction failed:', error);
  }
}
```

## Examples

### Complete LP Management Workflow

```typescript
import { Connection, PublicKey, Keypair } from '@solana/web3.js';
import { Program, BN } from '@coral-xyz/anchor';

class PumpFunManager {
  constructor(program: Program, wallet: Keypair) {
    this.program = program;
    this.wallet = wallet;
  }

  async addLiquidity(poolAddress: PublicKey, tokenMint: PublicKey, amount: number) {
    try {
      const tx = await this.program.methods
        .addVirtualLp(new BN(amount), tokenMint)
        .accounts({
          user: this.wallet.publicKey,
          pool: poolAddress,
        })
        .rpc();
      
      console.log('Liquidity added successfully:', tx);
      return tx;
    } catch (error) {
      console.error('Failed to add liquidity:', error);
      throw error;
    }
  }

  async removeLiquidity(poolAddress: PublicKey, tokenMint: PublicKey, amount: number) {
    try {
      const tx = await this.program.methods
        .removeVirtualLp(new BN(amount), tokenMint)
        .accounts({
          user: this.wallet.publicKey,
          pool: poolAddress,
        })
        .rpc();
      
      console.log('Liquidity removed successfully:', tx);
      return tx;
    } catch (error) {
      console.error('Failed to remove liquidity:', error);
      throw error;
    }
  }

  async createPool(tokenAMint: PublicKey, tokenBMint: PublicKey, liquidity: number) {
    try {
      const tx = await this.program.methods
        .createRaydiumPool(tokenAMint, tokenBMint, new BN(liquidity))
        .accounts({
          authority: this.wallet.publicKey,
          raydiumProgram: raydiumProgramId,
        })
        .rpc();
      
      console.log('Pool created successfully:', tx);
      return tx;
    } catch (error) {
      console.error('Failed to create pool:', error);
      throw error;
    }
  }
}
```

### Fee Management

```typescript
async function updatePoolFees(poolAddress: PublicKey, newFeeRate: number) {
  try {
    const tx = await program.methods
      .updatePoolFees(new BN(newFeeRate))
      .accounts({
        authority: wallet.publicKey,
        pool: poolAddress,
      })
      .rpc();
    
    console.log('Pool fees updated successfully:', tx);
    return tx;
  } catch (error) {
    console.error('Failed to update pool fees:', error);
    throw error;
  }
}
```

## Best Practices

### 1. Error Handling

Always implement proper error handling:

```typescript
try {
  const result = await program.methods.someMethod().rpc();
  // Handle success
} catch (error) {
  // Handle specific errors
  if (error.message.includes('specific error')) {
    // Handle specific error
  }
}
```

### 2. Transaction Confirmation

Always confirm transactions:

```typescript
const tx = await program.methods.someMethod().rpc();
await connection.confirmTransaction(tx);
```

### 3. Gas Optimization

Use appropriate gas limits:

```typescript
const tx = await program.methods
  .someMethod()
  .accounts({...})
  .rpc({ commitment: 'confirmed' });
```

### 4. Security Considerations

- Always validate inputs
- Use proper authorization checks
- Implement rate limiting where appropriate
- Keep private keys secure

## Rate Limits

The API implements the following rate limits:
- 100 requests per minute per IP
- 1000 requests per hour per wallet
- 10 pool creations per day per wallet

## Support

For API support:
- **Documentation**: [GitHub Wiki](https://github.com/Tronzit-Veca/Pumpfun-Smart-Contract/wiki)
- **Issues**: [GitHub Issues](https://github.com/Tronzit-Veca/Pumpfun-Smart-Contract/issues)
- **Telegram**: [@Tr1030109](https://t.me/Tr1030109)
- **Discord**: 0xapp123

---

**Last updated**: January 2024
**Version**: 1.0.0 