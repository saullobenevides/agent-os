# Plano: Sanitização de Erros v2 — Erros Silenciosos

> **Status:** ✅ CONCLUÍDO

---

## Correções Implementadas

### ALTA PRIORIDADE

| ID | Arquivo | Problema | Ação |
|---|---|---|---|
| A2 | `FotografoOnboarding.js` | `setSubmitError(err.message)` | → Mensagem fixa PT |
| B2 | `CartContext.js` | `addToCart` falha sem feedback | → `toast.error()` |
| B6 | `LocationSelector.js` | Estados/cidades vaziam sem aviso | → `toast.error()` × 2 |
| B10 | `pagamento/sucesso/page.js` | Pedido falha sem aviso | → Estado visual `fetchError` |
| EXTRA | `ConfigurarPagamentoClient.js` | `setSubmitError(err.message)` | → Mensagem fixa PT |

### MÉDIA PRIORIDADE

| ID | Arquivo | Problema | Ação |
|---|---|---|---|
| A1 | `FotografoOnboarding.js` | CEP fetch falha silencioso | → `toast.error()` |
| B5 | `CartContext.js` | Carrinho dessincronizado | → `toast.error()` |
| B7 | `UploadMetricsDashboard.js` | Dashboard vazio | → `toast.error()` |
| B8 | `SecurityDashboard.js` × 3 | 3 catches sem feedback | → `toast.error()` × 3 |
| B9 | `LegalComplianceDashboard.js` | Dashboard vazio | → `toast.error()` |

---

## Resumo

| Métrica | Valor |
|---|---|
| **Arquivos modificados** | 8 |
| **Pontos corrigidos** | 13 |
| **Toasts adicionados** | 11 |
| **Imports de `sonner` adicionados** | 4 |
| **Estados visuais de erro** | 1 |
| **err.message sanitizados** | 2 |
