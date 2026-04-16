# Response Format

## Route Handlers
```json
{ "data": { ... } }          // 200
{ "error": "mensagem" }      // 4xx/5xx
```
- Sempre incluir status HTTP correto (400, 401, 403, 404, 500)
- Nunca expor error.message, stack trace ou detalhes de validação Zod
- Mensagens de erro sempre em português

## Server Actions
```ts
return { success: true, data: serializeModel(result) }
return { error: "Mensagem genérica" }
```
- Nunca lançar exceção — sempre retornar `{ error }`
- Usar `serializeModel()` ao retornar dados do Prisma para o cliente
- Chamar `revalidatePath()` após mutações
