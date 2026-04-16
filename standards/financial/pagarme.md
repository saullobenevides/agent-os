# Pagar.me

- Toda integração via `lib/pagarme.js` — nunca chamar a API diretamente
- Valores SEMPRE em centavos (integer): R$ 10,50 = 1050
- Funções principais:
  - `createPixOrder({ amount, splits })` — cria pedido PIX com split
  - `createRecipient(...)` — cadastra recebedor (fotógrafo)
  - `createTransfer(recipientId, amount)` — saque
  - `getRecipientBalance(recipientId)` — saldo disponível
  - `verifyWebhookSignature(payload, sig)` — valida webhook
