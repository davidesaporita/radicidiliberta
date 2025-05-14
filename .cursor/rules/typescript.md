# TypeScript e Validazione dei Dati

## Principi Generali

- Usare **TypeScript** per tutto il codice
- Definire **tipi espliciti** per tutti i componenti e funzioni
- Implementare **validazione dei dati** con Zod
- Utilizzare **file types.ts separati** per definizioni di tipo condivise

## Organizzazione dei Tipi

```
lib/
├── types/
│   ├── common.ts     # Tipi condivisi in tutta l'app
│   ├── form.ts       # Tipi per i form
│   └── content.ts    # Tipi per i contenuti del sito
```

## Convenzioni di Denominazione

- **Interfaces/Types:** PascalCase
  ```ts
  interface UserData { ... }
  type FormSubmissionStatus = 'idle' | 'loading' | 'success' | 'error';
  ```
- **Generics:** PascalCase, singole lettere o descrittivi
  ```ts
  function getFirst<T>(items: T[]): T | undefined { ... }
  interface Pagination<ItemType> { ... }
  ```
- **Enums:** PascalCase
  ```ts
  enum ContentSectionId {
    Hero = 'hero',
    Problem = 'problem',
    Objectives = 'objectives',
  }
  ```

## Tipi Comuni

### Contenuti delle Sezioni

```ts
// lib/types/content.ts
export interface Section {
  id: string;
  title: string;
  subtitle?: string;
  content?: string;
  items?: string[];
  components: string[];
}

export interface ContentItem {
  id: string;
  title: string;
  description?: string;
  imageUrl?: string;
}
```

### Form e Validazione

```ts
// lib/types/form.ts
import { z } from 'zod';

export const ContactFormSchema = z.object({
  nome: z.string().min(2, "Il nome deve contenere almeno 2 caratteri"),
  email: z.string().email("Email non valida"),
  messaggio: z.string().min(10, "Il messaggio deve contenere almeno 10 caratteri"),
});

export type ContactFormData = z.infer<typeof ContactFormSchema>;
```

## Props per Componenti

```tsx
// components/SectionCard.tsx
import { Section } from '@/lib/types/content';

interface SectionCardProps {
  section: Section;
  variant?: 'default' | 'highlighted';
  withAnimation?: boolean;
}

export function SectionCard({ 
  section, 
  variant = 'default',
  withAnimation = true 
}: SectionCardProps) {
  // Component implementation
}
```

## Utility Types

```ts
// lib/types/common.ts
export type Nullable<T> = T | null;
export type Optional<T> = T | undefined;
export type AsyncData<T> = {
  data?: T;
  loading: boolean;
  error?: string;
};
```

## Best Practices

### Immutabilità
```ts
// Preferire
const updated = { ...original, property: newValue };

// Evitare
original.property = newValue;
```

### Type Guards
```ts
function isErrorResponse(response: any): response is ErrorResponse {
  return 'error' in response && typeof response.error === 'string';
}
```

### Inferenza dei Tipi
```ts
// Preferire l'inferenza quando chiaro
const sections = await getSections(); // Tipo inferito correttamente

// Specificare tipo quando necessario o per chiarezza
const section: Section = await getSection(id);
```

### Gestione degli Errori

```ts
// Definizione dell'errore
class ApiError extends Error {
  constructor(
    message: string,
    public status: number,
    public code?: string
  ) {
    super(message);
    this.name = 'ApiError';
  }
}

// Utilizzo
try {
  const data = await fetchData();
} catch (error) {
  if (error instanceof ApiError) {
    console.error(`API Error ${error.status}: ${error.message}`);
  } else {
    console.error('Unknown error:', error);
  }
}
``` 