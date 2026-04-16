# Formulários

Trio obrigatório: React Hook Form + Zod + `<Form>` do shadcn/ui

```tsx
const schema = z.object({ campo: z.string().min(1) });
const form = useForm({ resolver: zodResolver(schema) });

<Form {...form}>
  <FormField control={form.control} name="campo" render={({ field }) => (
    <FormItem>
      <FormLabel>Label</FormLabel>
      <FormControl><Input {...field} /></FormControl>
      <FormMessage />
    </FormItem>
  )} />
</Form>
```
- Nunca `<form>` nativo sem React Hook Form
- Validar com Zod antes de chamar Server Action
