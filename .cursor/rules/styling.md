# Stile e Design

## Palette Colori

```
- Primario:    #4CAF50 (Verde)
- Secondario:  #2E7D32 (Verde scuro)
- Accento:     #AED581 (Verde chiaro)
- Sfondo:      #F1F8E9 (Beige verdastro)
- Testo:       #212121 (Quasi nero)
```

## Tema Tailwind

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: '#4CAF50',
        secondary: '#2E7D32',
        accent: '#AED581',
        background: '#F1F8E9',
        text: '#212121',
      },
      borderRadius: {
        'lg': '1rem',
        'xl': '1.5rem',
        '2xl': '2rem',
      },
      boxShadow: {
        'md': '0px 4px 6px rgba(0,0,0,0.1)',
      }
    },
  },
}
```

## Componenti UI

### Cards
```tsx
// Esempio di utilizzo:
<div className="rounded-2xl shadow-md p-6 bg-background">
  {/* Card content */}
</div>
```

### Buttons
```tsx
// Button primario
<button className="px-6 py-3 rounded-lg font-semibold bg-primary text-white hover:bg-secondary">
  Invia
</button>

// Button secondario
<button className="px-6 py-3 rounded-lg font-semibold border-2 border-primary text-primary hover:bg-accent hover:text-secondary">
  Annulla
</button>
```

### Tipografia
```tsx
// Titoli
<h1 className="text-4xl font-bold text-primary mb-4">Titolo Principale</h1>
<h2 className="text-3xl font-bold text-secondary mb-3">Sottotitolo</h2>

// Testo
<p className="text-text text-lg leading-relaxed">Paragrafo standard</p>
<p className="text-secondary text-sm">Testo piccolo</p>
```

## Componenti shadcn/ui

Utilizzare i componenti shadcn/ui con la nostra palette personalizzata:

```tsx
// Esempio Button shadcn/ui
<Button variant="default" className="bg-primary hover:bg-secondary">
  Invia
</Button>
```

## Layout e Spaziature

- Utilizzare `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8` per contenitori principali
- Spaziatura tra sezioni: `py-16`
- Spaziatura tra elementi: `space-y-6`

## Responsive Design

- Mobile-first approach
- Breakpoints standard di Tailwind:
  - sm: 640px
  - md: 768px
  - lg: 1024px
  - xl: 1280px

## Animazioni e Transizioni

```css
/* globals.css */
@layer utilities {
  .transition-standard {
    @apply transition-all duration-300 ease-in-out;
  }
  
  .hover-scale {
    @apply hover:scale-105 transition-standard;
  }
}
```

## Immagini e Icone

- Immagini ottimizzate con next/image
- Icone da react-icons (preferibilmente set Heroicons o Phosphor Icons)
- SVG inline per icone personalizzate

## Accessibilità

- Contrasto minimo di 4.5:1 per il testo normale
- Contrasto minimo di 3:1 per il testo grande
- Tutti i componenti interattivi devono avere stato :focus visibile
- Utilizzare aria-labels per elementi non testuali 