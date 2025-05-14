# Framework: Next.js 15

## Principi Generali Next.js

- Utilizziamo **Next.js 15** con **App Router**
- Preferiamo **Server Components** per default
- Usiamo **Server Actions** per la manipolazione dei dati
- Implementiamo **Streaming** per componenti con caricamento progressivo

## Struttura delle Route

```
app/
├── layout.tsx       # Layout principale con metadata
├── page.tsx         # Homepage
├── contact/
│   └── page.tsx     # Pagina contatti
├── about/
│   └── page.tsx     # Pagina chi siamo
└── components/      # Componenti condivisi
```

## Best Practices

- **Server vs Client:**
  - Tutti i componenti sono **Server Components** per default
  - Aggiungere `'use client';` solo quando necessario
  - Aggiungere `import 'server-only';` ai file con dati sensibili

- **Data Fetching:**
  - Preferire data fetching nei Server Components
  - Evitare API Routes quando possibile
  - Utilizzare fetch con opzioni di caching appropriate

- **Form e Mutazioni:**
  - Utilizzare Server Actions per gestire form e mutazioni
  - Validare input con Zod sia lato client che server

- **Rendering e Performance:**
  - Implementare correttamente Static vs Dynamic rendering
  - Utilizzare streaming per componenti pesanti
  - Implementare correttamente la revalidazione dei dati

- **Navigazione:**
  - Utilizzare `next/navigation` (non `next/router`)
  - Preferire Link component per navigazione interna
  - Implementare correttamente i layout nidificati

## Esempi

### Server Component
```tsx
// app/page.tsx
import { getProgetti } from '@/lib/data';

export default async function HomePage() {
  const progetti = await getProgetti();
  
  return (
    <div>
      <h1>Radici di Libertà</h1>
      {progetti.map(progetto => (
        <ProgettoCard key={progetto.id} progetto={progetto} />
      ))}
    </div>
  );
}
```

### Server Action
```tsx
// app/actions.ts
'use server';

import { z } from 'zod';
import { revalidatePath } from 'next/cache';

const ContactSchema = z.object({
  nome: z.string().min(2),
  email: z.string().email(),
  messaggio: z.string().min(10),
});

export async function inviaMessaggio(formData: FormData) {
  const rawData = {
    nome: formData.get('nome'),
    email: formData.get('email'),
    messaggio: formData.get('messaggio'),
  };
  
  const validatedData = ContactSchema.parse(rawData);
  
  // Logica per salvare il messaggio
  await salvaNelDatabase(validatedData);
  
  revalidatePath('/contact');
  return { success: true };
}
```

### Client Component
```tsx
// components/ContactForm.tsx
'use client';

import { useForm } from 'react-hook-form';
import { inviaMessaggio } from '@/app/actions';

export function ContactForm() {
  const { register, handleSubmit, formState } = useForm();
  
  return (
    <form action={inviaMessaggio}>
      {/* Form fields */}
    </form>
  );
}
``` 