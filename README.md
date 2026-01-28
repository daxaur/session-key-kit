# session key kit

toolkit for implementing session keys in your dapp. sign once, execute many.

**status:** planning phase. research repo for now.

---

## what are session keys?

web2: login once, stay logged in  
web3: sign once, automate forever

ctrl uses session keys for automation. this would help other devs do the same.

---

## planned features

```typescript
import { SessionKeyManager } from 'session-key-kit'

const manager = new SessionKeyManager(wallet)

// create session key
const key = await manager.create({
  permissions: ['swap', 'transfer'],
  expiresIn: '30d',
  rateLimit: 100
})

// execute with session key
await manager.execute(key, { action: 'swap', params: {...} })
```

---

## why?

session keys enable defi automation. but security is hard. this would provide:
- encryption patterns
- best practices
- example implementations
- security guidelines

---

## when?

after ctrl proves the pattern works. maybe open source ctrl's session key implementation.

---

building in public: [@daxaur](https://x.com/daxaur)
