# Referências para Sanitização de Erros

## Implementações de Referência

### Padrão correto já existente — `api/checkout/create-payment-intent/route.js`

- **Localização:** `app/api/checkout/create-payment-intent/`
- **Relevância:** Rota que já segue o padrão corretamente
- **Padrão:** Todos os catch blocks retornam mensagens genéricas em português, logam o erro real via `logError()`, nunca expõem `error.message`

### Padrão correto — Server Actions (`actions/*.ts`)

- **Localização:** `actions/`
- **Relevância:** Nenhuma action expõe `error.message` — todas retornam `{ error: "mensagem em português" }`
- **Padrão:** O padrão de actions está limpo e pode servir de referência

### Padrão de erros do framework — `agent-os/standards/api/`

- **Localização:** `agent-os/standards/api/response-format.md`, `auth-and-validation.md`
- **Relevância:** Define o padrão que deve ser seguido em todas as rotas
