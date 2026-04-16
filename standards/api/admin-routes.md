# Rotas Admin

```ts
import { requireAdminApi, logAdminActivity } from "@/lib/admin/permissions";

export async function POST(request) {
  const { user, error } = await requireAdminApi(); // auth + role check
  if (error) return error; // já retorna NextResponse com status

  // ... lógica ...

  await logAdminActivity(user.id, "approve_saque", { saqueId, valor });
  return NextResponse.json({ data: result });
}
```

- `requireAdminApi()` — primeira chamada em toda rota admin, verifica auth + role ADMIN
- `logAdminActivity()` — obrigatório após toda mutação (aprovar, rejeitar, deletar, atualizar)
- Leitura (GET/listagem) pode pular o log, mutações nunca pulam
- Não usar em Server Actions normais — apenas em route handlers do painel admin
