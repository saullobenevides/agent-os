# Plano: Sanitização de Erros — GTClicks

> **Spec:** `agent-os/specs/2026-04-14-2223-error-sanitization/`
> **Status:** ✅ CONCLUÍDO

---

## Task 1: Salvar documentação da spec ✅

## Task 2: Corrigir `error.message` vazando em API Routes ✅
- `fotografos/pagamento/status/route.js` — removido `error?.message`
- `admin/reconciliation/route.js` — removido `error?.message`

## Task 3: Traduzir mensagens em inglês nas API Routes ✅
**Rotas corrigidas (12):**
- `webhooks/pagarme/route.js` (4 mensagens)
- `users/sync/route.js` (2)
- `users/me/route.js` (2)
- `users/me/likes/route.js` (2)
- `photos/[id]/like/route.js` (2)
- `test-data/route.js` (1)
- `carrinho/route.js` (2)
- `carrinho/item/route.js` (2)
- `carrinho/sync/route.js` (2)
- `auth/sync/route.js` (3)
- `auth/code/send/route.js` (2)
- `cron/reconciliation/route.js` (2)
- `folders/route.js` (2)
- `folders/[id]/route.js` (2)

## Task 4: Remover IDs internos e termos técnicos ✅
- `pedidos/route.js` — "Item sem fotoId" → "Item inválido no pedido", `${item.fotoId}` removido
- `upload/route.js` — "S3 nao configurado" → "Serviço de upload temporariamente indisponível"
- `fotografos/create/route.js` — `parseResult.error.message` → mensagem fixa
- `folders/route.js` — `parsed.error.issues[0].message` → "Dados inválidos"
- `colecoes/route.js` — `parsed.error.issues[0].message` → "Dados inválidos"
- `colecoes/[id]/route.js` — `parsed.error.issues[0].message` → "Dados inválidos"
- `carrinho/item/route.js` — `parseResult.error.message` → "Dados do item inválidos"

## Task 5: Corrigir acentuação ✅
- `upload/route.js` — "Nao autorizado" → "Não autorizado"
- `pedidos/route.js` — "Nao autorizado" × 2
- `pedidos/[id]/route.js` — "Nao autorizado"
- `colecoes/route.js` — "Nao foi possivel" × 2
- `colecoes/[id]/route.js` — "Nao autorizado" × 2, "fotografo nao encontrado"

## Task 6: Sanitizar erros no client-side ✅
- `FolderManager.js` — 4× `setError(err.message)` → mensagens fixas
- `CollectionEditor.js` — 6× `toast.error(error.message)` → mensagens fixas
- `usePhotoUpload.js` — 1× `toast.error(error.message)` → mensagem fixa
- `admin/financeiro/page.js` — 1× `toast.error(error.message)` → mensagem fixa + MercadoPago→Pagar.me

## Task 7: Garantir logError() em catch blocks ✅
- `colecoes/route.js` — adicionado import + 2 chamadas logError
- `pedidos/route.js` — adicionado logError no GET

## Task 8: Atualizar testes ✅
- 6 asserções de testes atualizadas: "Unauthorized" → "Não autorizado"

---

## Resumo Final

| Métrica | Valor |
|---|---|
| **Arquivos de código modificados** | 26 |
| **Pontos de erro corrigidos** | ~55 |
| **Mensagens EN → PT** | ~30 |
| **error.message removidos** | 14 |
| **Zod issues removidos** | 5 |
| **Acentuação corrigida** | ~12 |
| **logError adicionados** | 3 |
| **Testes atualizados** | 4 |
