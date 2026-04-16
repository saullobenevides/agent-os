# Valores Monetários

## Prisma.Decimal
```ts
import { Prisma } from "@prisma/client";

const share = new Prisma.Decimal(1).sub(new Prisma.Decimal(taxa).div(100));
const valorFotografo = new Prisma.Decimal(precoPago).mul(share);
```
- NUNCA usar `number` para valores monetários (perde precisão)
- Armazena no banco como Decimal, serializa com `serializeModel()`

## $transaction
```ts
await prisma.$transaction(async (tx) => {
  await tx.pedido.update(...);
  await tx.saldo.update(...);
  await tx.transacao.create(...);
});
```
- Obrigatório em toda operação que movimenta saldo

## Webhook como fonte de verdade
- NUNCA marcar pedido como PAGO por polling ou ação do usuário
- Apenas `order.paid` do webhook Pagar.me atualiza status para PAGO
- Handler em `lib/process-order-paid.js`
