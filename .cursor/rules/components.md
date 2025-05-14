# Componenti UI

## Struttura dei Componenti

```
components/
├── ui/               # Componenti UI generici e riutilizzabili
│   ├── button.tsx
│   ├── card.tsx
│   └── input.tsx
├── sections/         # Sezioni principali della pagina
│   ├── hero.tsx
│   ├── problem-section.tsx
│   └── objectives-section.tsx
├── layout/           # Componenti di layout
│   ├── header.tsx
│   └── footer.tsx
└── forms/            # Componenti per form
    └── contact-form.tsx
```

## Componenti Principali

### Header
```tsx
// components/layout/header.tsx
import { Link } from 'next/link';
import { Button } from '@/components/ui/button';

export function Header() {
  return (
    <header className="bg-background py-4 shadow-sm">
      <nav className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex justify-between items-center">
        <Link href="/" className="flex items-center">
          <span className="text-xl font-bold text-primary">Radici di Libertà</span>
        </Link>
        
        <div className="flex gap-4">
          <Link href="/#objectives">Obiettivi</Link>
          <Link href="/#activities">Attività</Link>
          <Link href="/#contact">
            <Button variant="default">Contatti</Button>
          </Link>
        </div>
      </nav>
    </header>
  );
}
```

### Hero
```tsx
// components/sections/hero.tsx
import Image from 'next/image';
import { Button } from '@/components/ui/button';

export function Hero() {
  return (
    <section className="relative h-[80vh] flex items-center">
      {/* Background image */}
      <div className="absolute inset-0 z-0">
        <Image
          src="/images/hero-bg.jpg"
          alt="Immagine di natura rigogliosa"
          fill
          className="object-cover"
          priority
        />
        <div className="absolute inset-0 bg-primary/30" />
      </div>
      
      {/* Content */}
      <div className="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-white">
        <h1 className="text-4xl md:text-5xl lg:text-6xl font-bold mb-4">
          Radici di Libertà
        </h1>
        <p className="text-xl md:text-2xl mb-8 max-w-xl">
          Rigenerare possibilità e benessere attraverso la natura
        </p>
        <Button size="lg" className="bg-white text-primary hover:bg-accent hover:text-secondary">
          Scopri il progetto
        </Button>
      </div>
    </section>
  );
}
```

### SectionCard
```tsx
// components/sections/section-card.tsx
import { Section } from '@/lib/types/content';
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';

interface SectionCardProps {
  section: Section;
  className?: string;
}

export function SectionCard({ section, className = '' }: SectionCardProps) {
  return (
    <Card className={`rounded-2xl shadow-md ${className}`}>
      <CardHeader>
        <CardTitle className="text-2xl font-bold text-primary">{section.title}</CardTitle>
        {section.subtitle && (
          <p className="text-lg text-secondary">{section.subtitle}</p>
        )}
      </CardHeader>
      <CardContent>
        {section.content && <p className="mb-4">{section.content}</p>}
        
        {section.items && (
          <ul className="space-y-2">
            {section.items.map((item, index) => (
              <li key={index} className="flex gap-2">
                <span className="text-accent">•</span>
                <span>{item}</span>
              </li>
            ))}
          </ul>
        )}
      </CardContent>
    </Card>
  );
}
```

### ContactForm
```tsx
// components/forms/contact-form.tsx
'use client';

import { useState } from 'react';
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { ContactFormSchema, ContactFormData } from '@/lib/types/form';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Textarea } from '@/components/ui/textarea';
import { inviaMessaggio } from '@/app/actions';

export function ContactForm() {
  const [status, setStatus] = useState<'idle' | 'submitting' | 'success' | 'error'>('idle');
  
  const { 
    register, 
    handleSubmit, 
    formState: { errors },
    reset
  } = useForm<ContactFormData>({
    resolver: zodResolver(ContactFormSchema)
  });
  
  async function onSubmit(data: ContactFormData) {
    try {
      setStatus('submitting');
      await inviaMessaggio(data);
      setStatus('success');
      reset();
    } catch (error) {
      console.error('Errore durante l\'invio:', error);
      setStatus('error');
    }
  }
  
  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <div>
        <label htmlFor="nome" className="block mb-1">Nome</label>
        <Input 
          id="nome"
          {...register('nome')}
          aria-invalid={errors.nome ? 'true' : 'false'}
        />
        {errors.nome && (
          <p className="text-red-500 text-sm mt-1">{errors.nome.message}</p>
        )}
      </div>
      
      <div>
        <label htmlFor="email" className="block mb-1">Email</label>
        <Input
          id="email"
          type="email"
          {...register('email')}
          aria-invalid={errors.email ? 'true' : 'false'}
        />
        {errors.email && (
          <p className="text-red-500 text-sm mt-1">{errors.email.message}</p>
        )}
      </div>
      
      <div>
        <label htmlFor="messaggio" className="block mb-1">Messaggio</label>
        <Textarea
          id="messaggio"
          rows={5}
          {...register('messaggio')}
          aria-invalid={errors.messaggio ? 'true' : 'false'}
        />
        {errors.messaggio && (
          <p className="text-red-500 text-sm mt-1">{errors.messaggio.message}</p>
        )}
      </div>
      
      <Button 
        type="submit" 
        className="w-full"
        disabled={status === 'submitting'}
      >
        {status === 'submitting' ? 'Invio in corso...' : 'Invia Messaggio'}
      </Button>
      
      {status === 'success' && (
        <p className="text-green-600 text-center">Messaggio inviato con successo!</p>
      )}
      
      {status === 'error' && (
        <p className="text-red-600 text-center">Si è verificato un errore. Riprova più tardi.</p>
      )}
    </form>
  );
}
```

## Best Practices per i Componenti

### Responsabilità Singola
- Ogni componente dovrebbe avere una singola responsabilità
- Estrarre logica complessa in custom hooks
- Separare presentazione e logica quando possibile

### Riutilizzabilità
- Progettare componenti per essere riutilizzabili
- Parametrizzare varianti e stili
- Utilizzare props con valori di default

### Accessibilità
- Utilizzare elementi semantici HTML
- Includere attributi ARIA quando necessario
- Garantire navigabilità da tastiera
- Testare con screen reader

### Performance
- Evitare re-render non necessari
- Utilizzare `memo` per componenti costosi
- Utilizzare Suspense per caricamento asincrono
- Lazy load componenti pesanti 