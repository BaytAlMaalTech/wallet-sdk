# wallet-sdk

> 💼 TypeScript/JavaScript SDK for Islamic banks to integrate with SHARIAH OVERLORD

[![npm](https://img.shields.io/npm/v/@baytalmaalttech/sovereign-wallet-sdk)](https://www.npmjs.com/package/@baytalmaalttech/sovereign-wallet-sdk)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)

## Installation

```bash
npm install @baytalmaalttech/sovereign-wallet-sdk
# or
yarn add @baytalmaalttech/sovereign-wallet-sdk
```

## Quick Start

```typescript
import { createSovereignClient } from '@baytalmaalttech/sovereign-wallet-sdk';

const client = createSovereignClient({
  gatewayUrl: 'https://api.shariahoverlord.io',
  authToken: process.env.SOVEREIGN_AUTH_TOKEN!,
  institutionId: 'bank_mandiri_syariah_ID',
});

// Submit a Murabahah transaction
const result = await client.submitTransaction({
  from: '0xabc...',
  to: '0xdef...',
  amount: '10000000',  // IDR 100,000
  currency: 'IDR',
  akad: 'Murabahah',
  memo: 'Home furniture — cost + 15% markup disclosed',
});

console.log(result.shariahStatus); // 'HALAL'

// Check Zakat obligation
const zakat = await client.getZakatAssessment('0xabc...');
if (zakat.zakatObligatory) {
  console.log(`Zakat due: ${zakat.zakatAmount} ${zakat.currency}`);
}

// Verify banknote authenticity
const check = await client.verifyNote({
  serial: 'IDR100000-2024-ABC123456',
  currency: 'IDR',
  denomination: 100000,
  issueYear: 2024,
  issuingAuthority: 'ID',
});
console.log(check.verdict); // 'AUTHENTIC'
```

## Supported Akad Types

Mudarabah, Musharakah, MusharakahMutanaqisah, Murabahah, Tawarruq, Salam, Istisna, Ijarah, IjarahMuntahia, Wakalah, Wadiah, Qard, Kafalah, Hawalah, Hibah, Sadaqah, Zakat, Waqf

## License

MIT — free to use in any Islamic banking application

---
*© 2026 BaytAlMaalTech*
