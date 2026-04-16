# Rate Limiting

Ordem obrigatória nas rotas protegidas:

```ts
// 1. IP limiter ANTES da auth
const ip = getClientIp(request);
const { allowed } = await uploadLimiter(ip); // ou checkoutLimiter
if (!allowed) return tooManyRequestsResponse();

// 2. Auth
const user = await getAuthenticatedUser();
if (!user) return NextResponse.json({ error: "Não autorizado" }, { status: 401 });

// 3. Quota por usuário (após auth)
const kv = await kvCheck(`upload:${user.id}`, 20, 60);
if (kv && !kv.allowed) return tooManyRequestsResponse();
```

Limitadores disponíveis em `@/lib/rate-limit`:
- `uploadLimiter` — rotas de upload de fotos
- `checkoutLimiter` — rotas de checkout/pagamento
- `kvCheck(key, limit, windowSec)` — quota por usuário autenticado

IP limiter DEVE vir antes da auth — protege contra ataques externos sem custo de DB.
