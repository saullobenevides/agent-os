# UI Components

- SEMPRE usar componentes shadcn/ui (`@/components/ui/*`)
- NUNCA usar `<button>` nativo — sempre `Button` do shadcn/ui
- NUNCA cores hard-coded (`text-white`, `bg-black`, `#fff`) — usar variáveis CSS do tema
  - Correto: `bg-primary`, `text-foreground`, `border-border`, `text-muted-foreground`
- Dark mode por padrão
- SEMPRE `Image` do Next.js para imagens (nunca `<img>`)
- Um componente por arquivo
