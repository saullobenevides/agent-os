# Stack Auth

```ts
// Client Component
"use client";
import { useUser } from "@stackframe/stack";
const user = useUser({ or: "redirect" }); // redireciona para /handler/sign-in

// Server Component / Action / Route Handler
import { getAuthenticatedUser } from "@/lib/auth";
const user = await getAuthenticatedUser();
if (!user) return { error: "Não autorizado" };
```
- Nunca usar middleware para auth
- Nunca misturar: useUser() é apenas client-side
