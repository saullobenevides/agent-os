# Autenticação e Validação

## Autenticação
```ts
// Route Handlers & Server Actions
const user = await getAuthenticatedUser(); // de @/lib/auth
if (!user) return { error: "Não autorizado" }; // ou NextResponse 401
```
- Client Components: `useUser()` do `@stackframe/stack`
- Nunca usar middleware para verificar auth

## Validação Zod
```ts
const result = schema.safeParse(data);
if (!result.success) {
  // Route Handler: erro genérico apenas
  return NextResponse.json({ error: "Dados inválidos" }, { status: 400 });
  // Server Action: pode retornar fieldErrors para destacar campos
  return { error: "Dados inválidos", fieldErrors: result.error.flatten().fieldErrors };
}
```
- Route Handlers: sempre `{ error: string }` genérico (nunca detalhes Zod)
- Server Actions: PODE retornar `fieldErrors` — são erros de validação, não internos
- NUNCA expor: error.message de catch, stack trace, erros de DB
- Sempre `logError(error, context)` no catch antes de retornar genérico
