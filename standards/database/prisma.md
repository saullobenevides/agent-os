# Prisma

- `serializeModel(data)` de `@/lib/serialization` ao passar Prisma data para Client Components
  (converte Decimal, Date, BigInt para JSON-safe)
- `dayjs` para toda manipulação e formatação de datas — nunca `new Date()` diretamente na UI
- Acesso ao banco apenas em Server Components, Server Actions ou Route Handlers
  (nunca em Client Components)
