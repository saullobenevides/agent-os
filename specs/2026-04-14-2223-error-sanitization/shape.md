# Sanitização de Erros — Shaping Notes

## Escopo

Limpeza e sanitização de **todas** as mensagens de erro exibidas ao usuário final (incluindo admin), garantindo:
- Linguagem clara em português brasileiro
- Zero termos técnicos expostos (error.message, stack traces, IDs internos)
- Mensagens contextuais que indicam o *tipo* do problema sem detalhes internos

## Problemas Encontrados

### Categoria A — `error.message` vazando em API Routes (2 rotas)

| Arquivo | Linha | Código atual |
|---|---|---|
| `api/fotografos/pagamento/status/route.js` | 71 | `{ error: error?.message \|\| "Erro ao verificar status" }` |
| `api/admin/reconciliation/route.js` | 108 | `{ error: error?.message \|\| "Erro na reconciliação" }` |

**Risco:** Mensagens de erro do Prisma, Node.js ou serviços externos podem vazar para o usuário.

### Categoria B — Mensagens em inglês nas API Routes (16+ rotas)

| Arquivo | Mensagem em inglês |
|---|---|
| `api/webhooks/pagarme/route.js` | "Invalid token", "Invalid payload", "Event not confirmed", "Webhook processing failed" |
| `api/users/sync/route.js` | "Not authenticated", "Failed to sync user" |
| `api/users/me/route.js` | "Not authenticated", "Internal server error" |
| `api/users/me/likes/route.js` | "Unauthorized", "Internal Server Error" |
| `api/photos/[id]/like/route.js` | "Unauthorized", "Internal Server Error" |
| `api/test-data/route.js` | "Not found" |
| `api/pedidos/route.js` | "Item sem fotoId", `Foto não encontrada: ${item.fotoId}` (vaza ID interno) |

### Categoria C — `error.message` em toast/setState no client-side (12 pontos)

| Arquivo | Linhas | Padrão |
|---|---|---|
| `features/collections/components/FolderManager.js` | 69, 104, 123, 137 | `setError(err.message)` |
| `features/collections/components/CollectionEditor.js` | 149, 249, 414, 453, 608, 675 | `toast.error(error.message \|\| "...")` |
| `features/collections/hooks/usePhotoUpload.js` | 353 | `` toast.error(`Erro ao processar imagem: ${error.message}`) `` |
| `app/admin/financeiro/page.js` | 43 | `toast.error(error.message)` |

### Categoria D — Mensagens sem acento / inconsistentes

| Arquivo | Mensagem |
|---|---|
| `api/upload/route.js` | "Nao autorizado" (falta acento), "S3 nao configurado." (técnico) |
| `api/pedidos/route.js` | "Nao autorizado" (falta acento) |
| `api/pedidos/[id]/route.js` | "Nao autorizado" (falta acento) |

## Decisões

1. **Todas as rotas admin também são sanitizadas** — mensagens em português, sem termos técnicos
2. **Mensagens contextuais** — indicam o tipo do problema (ex: "Não foi possível processar o pagamento") em vez de genéricas
3. **Webhook do Pagar.me** pode manter mensagens em inglês internamente (não são exibidas ao usuário), mas formatar as que chegam via API
4. **`error.message` nunca deve ser exibido ao usuário** — sempre substituir por mensagem fixa em português
5. **IDs internos nunca expostos** — ex: `Foto não encontrada: ${item.fotoId}` → apenas "Foto não encontrada"

## Context

- **Visuais:** Nenhum necessário
- **Referências:** O padrão já existe em `agent-os/standards/api/response-format.md` e `auth-and-validation.md`, mas não está sendo seguido em ~30 pontos
- **Produto:** N/A

## Standards Aplicados

- `api/response-format` — Formato de resposta e tratamento de erros
- `api/auth-and-validation` — O que expor vs esconder em erros
