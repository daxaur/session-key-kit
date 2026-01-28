# session key kit

toolkit for implementing session keys in your dapp. examples, best practices, security guidelines.

## what are session keys?

session keys enable "sign once, execute many" workflows. users sign a session key creation tx, then the session key can execute approved actions on their behalf.

think of it like:
- web2: login once, stay logged in
- web3: sign once, automate forever

## features

- session key generation utilities
- on-chain session manager contracts
- security best practices
- expiration + revocation patterns
- rate limiting integration
- examples for common use cases

## installation

```bash
npm install session-key-kit
```

## usage

### create a session key

```typescript
import { SessionKeyManager } from 'session-key-kit'

const manager = new SessionKeyManager({
  wallet: userWallet,
  provider: ethersProvider
})

const sessionKey = await manager.create({
  permissions: ['swap', 'transfer'],
  expiresIn: '30d',
  rateLimit: 100 // max 100 operations
})
```

### execute with session key

```typescript
const tx = await manager.execute(sessionKey, {
  action: 'swap',
  params: {
    tokenIn: 'USDC',
    tokenOut: 'ETH',
    amount: '100'
  }
})
```

### revoke session key

```typescript
await manager.revoke(sessionKey.id)
```

## security

session keys are powerful. here's how to use them safely:

### encryption
- always encrypt session keys at rest
- use aes-256-gcm minimum
- unique salt per key
- never store plaintext

### expiration
- set reasonable expiration (30 days max recommended)
- implement auto-rotation for long-running automation
- require re-auth after expiration

### permissions
- grant minimum necessary permissions
- use action whitelisting
- implement spending limits
- add time-based restrictions

### rate limiting
- prevent abuse with rate limits
- implement cooldowns
- track execution count
- circuit breaker pattern

### revocation
- allow instant revocation
- implement emergency pause
- notify on suspicious activity
- audit all executions

## examples

check `/examples` for complete implementations:
- defi automation (ctrl use case)
- gaming auto-play
- social media bots
- recurring payments

## smart contracts

session key manager contracts in `/contracts`:
- session creation
- permission management
- execution validation
- rate limiting

audited by: pending

## best practices

1. **never share session keys** - treat like private keys
2. **encrypt at rest** - always use strong encryption
3. **set expiration** - 30 days max for high-value operations
4. **limit permissions** - whitelist specific actions only
5. **rate limit** - prevent runaway execution
6. **monitor usage** - alert on unusual activity
7. **easy revocation** - one-click disable
8. **audit logs** - track every execution

## architecture

```
user wallet
    ↓ (signs once)
session key
    ↓ (executes many)
your protocol
```

## faq

**q: are session keys safe?**  
a: yes, if implemented correctly. follow security guidelines.

**q: what if session key is compromised?**  
a: revoke immediately. limit damage with permissions + rate limits.

**q: can session keys access my full wallet?**  
a: no. only approved actions within defined limits.

**q: how long should session keys last?**  
a: 30 days max for high-value operations. less for critical actions.

---

built for ctrl, useful for everyone.
