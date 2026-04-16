# Standards para Sanitização de Erros

Os seguintes standards aplicam-se a este trabalho.

---

## api/response-format

### Route Handlers
```json
{ "data": { ... } }          // 200
{ "error": "mensagem" }      // 4xx/5xx
```
- Sempre incluir status HTTP correto (400, 401, 403, 404, 500)
- Nunca expor error.message, stack trace ou detalhes de validação Zod
- Mensagens de erro sempre em português

### Server Actions
```ts
return { success: true, data: serializeModel(result) }
return { error: "Mensagem genérica" }
```
- Nunca lançar exceção — sempre retornar `{ error }`
- Usar `serializeModel()` ao retornar dados do Prisma para o cliente
- Chamar `revalidatePath()` após mutações

---

## api/auth-and-validation

### Autenticação
```ts
const user = await getAuthenticatedUser();
if (!user) return { error: "Não autorizado" }; // ou NextResponse 401
```

### Validação Zod
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
