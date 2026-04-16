# Roles

| Role | Acesso |
|---|---|
| CLIENTE | Compra fotos, pedidos, downloads |
| FOTOGRAFO | CLIENTE + upload, dashboard, saques |
| ADMIN | Acesso total |

- Role fica em `user.role` (Prisma User)
- Verificar role em Server Actions: `if (user.role !== "ADMIN") return { error: "Acesso negado" }`
- Rotas admin: usar `requireAdminApi()` de `@/lib/admin/permissions`
