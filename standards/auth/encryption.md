# Criptografia de Campos

- CPF e chave Pix SEMPRE criptografados via `prisma-field-encryption`
- Campos marcados no schema com `/// @encrypted` são cifrados automaticamente
- Toda criptografia é gerenciada pelo middleware do Prisma — não há encrypt/decrypt manual
- Nunca armazenar CPF ou chave Pix em texto puro
