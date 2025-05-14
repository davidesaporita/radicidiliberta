# Stile Grafico Ispirato al Poster Scientifico

## Adattamento della Palette Colori

Basandoci sul poster scientifico fornito, potrebbe essere necessario affinare la nostra palette colori per mantenere coerenza visiva:

```js
// tailwind.config.js - aggiornamento della palette dai colori del poster
module.exports = {
  theme: {
    extend: {
      colors: {
        // Esempio di palette raffinata basata sul poster
        primary: {
          DEFAULT: '#4CAF50', // Verde principale
          light: '#81C784',   // Verde chiaro per sfumature
          dark: '#2E7D32',    // Verde scuro per contrasti
        },
        secondary: {
          DEFAULT: '#388E3C', // Verde intermedio
          light: '#66BB6A',
          dark: '#1B5E20',
        },
        accent: {
          DEFAULT: '#AED581', // Verde accent
          light: '#C5E1A5',
          dark: '#8BC34A',
        },
        background: {
          DEFAULT: '#F1F8E9', // Beige verdastro
          alt: '#E8F5E9',     // Alternativo per sezioni
        },
        text: {
          DEFAULT: '#212121', // Testo principale
          light: '#757575',   // Testo secondario
        }
      }
    }
  }
}
```

## Tipografia Coordinata

Per allinearsi allo stile del poster, utilizziamo una combinazione di font che riproducano l'aspetto del poster scientifico:

```js
// tailwind.config.js - estensione per typography
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        // Individuare font simili a quelli del poster
        sans: ['Inter', 'system-ui', 'sans-serif'],
        display: ['Montserrat', 'system-ui', 'sans-serif'],
        heading: ['Poppins', 'system-ui', 'sans-serif'],
      },
    }
  }
}
```

## Elementi Grafici Distintivi

### Forme Organiche
```css
/* globals.css */
.organic-shape-top {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 6rem;
  background-image: url('/images/shapes/wave-top.svg');
  background-size: cover;
  background-repeat: no-repeat;
}

.organic-shape-bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 6rem;
  background-image: url('/images/shapes/wave-bottom.svg');
  background-size: cover;
  background-repeat: no-repeat;
}
```

### Componente Card con Stile del Poster
```tsx
// components/ui/poster-card.tsx
import { ReactNode } from 'react';
import { cn } from '@/lib/utils';

interface PosterCardProps {
  children: ReactNode;
  className?: string;
  variant?: 'primary' | 'secondary' | 'accent';
}

export function PosterCard({ 
  children, 
  className, 
  variant = 'primary' 
}: PosterCardProps) {
  return (
    <div className={cn(
      "rounded-3xl p-8 relative overflow-hidden shadow-md",
      variant === 'primary' && "bg-gradient-to-br from-primary-light to-primary",
      variant === 'secondary' && "bg-gradient-to-br from-secondary-light to-secondary",
      variant === 'accent' && "bg-gradient-to-br from-accent-light to-accent",
      className
    )}>
      {/* Elemento grafico organico */}
      <div className="absolute top-0 right-0 w-24 h-24 opacity-10 pointer-events-none">
        <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <path fill="#FFFFFF" d="M42.3,-68.5C52.1,-61.9,55.4,-44.2,62.5,-28.2C69.7,-12.3,80.8,1.9,81.7,16.5C82.6,31.1,73.3,46.1,60.4,55.6C47.6,65.1,31.1,69.1,15.4,70.7C-0.3,72.3,-15.3,71.5,-29.6,66.2C-43.9,61,-57.6,51.3,-66.4,38.1C-75.2,24.9,-79.2,8.3,-76.5,-6.9C-73.8,-22.1,-64.4,-35.9,-52.7,-43.8C-41,-51.6,-26.9,-53.5,-13.9,-59.8C-0.9,-66.1,10.9,-76.7,23.5,-77.9C36,-79,48.2,-71,42.3,-68.5Z" transform="translate(100 100)" />
        </svg>
      </div>
      
      {children}
    </div>
  );
}
```

## Layout e Sezioni come nel Poster

### Hero Section Stile Poster
```tsx
// components/sections/poster-hero.tsx
import Image from 'next/image';

export function PosterHero() {
  return (
    <section className="relative min-h-[90vh] bg-gradient-to-b from-primary-dark to-primary">
      {/* Pattern di foglie sovrapposto */}
      <div className="absolute inset-0 opacity-20 pointer-events-none">
        <Image 
          src="/images/patterns/leaves-pattern.png"
          alt=""
          fill
          className="object-cover"
          aria-hidden="true"
        />
      </div>
      
      <div className="relative z-10 container mx-auto px-4 pt-20 pb-32 flex flex-col justify-center h-full">
        {/* Titolo grande come nel poster */}
        <div className="max-w-3xl">
          <h1 className="font-heading text-5xl md:text-7xl font-bold text-white mb-8">
            Radici di Libertà
          </h1>
          <p className="text-xl md:text-2xl text-white/90 mb-12 max-w-xl leading-relaxed">
            Rigenerare possibilità e benessere attraverso la natura
          </p>
          
          {/* Box informativo come nel poster */}
          <div className="bg-white/20 backdrop-blur-sm rounded-2xl p-6 border border-white/30">
            <p className="text-white font-medium">
              Un progetto di ecologia carceraria per il benessere, la riduzione dello stress e il reinserimento sociale
            </p>
          </div>
        </div>
      </div>
      
      {/* Separatore curvo in basso, simile al poster */}
      <div className="absolute bottom-0 left-0 w-full h-16 overflow-hidden">
        <svg viewBox="0 0 1200 120" preserveAspectRatio="none" className="absolute bottom-0 left-0 w-full h-full">
          <path fill="#F1F8E9" d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V120H0V95.8C59.71,118.92,146.5,85.03,216.23,70.28,289.62,55.07,262.41,67.23,321.39,56.44Z"></path>
        </svg>
      </div>
    </section>
  );
}
```

## Icone e Illustrazioni

### Set di Icone Personalizzate
```tsx
// components/ui/eco-icon.tsx
interface EcoIconProps {
  name: 'leaf' | 'tree' | 'plant' | 'water' | 'sun';
  size?: 'sm' | 'md' | 'lg';
  className?: string;
}

export function EcoIcon({ name, size = 'md', className = '' }: EcoIconProps) {
  const sizeClasses = {
    sm: 'w-5 h-5',
    md: 'w-6 h-6',
    lg: 'w-8 h-8'
  };
  
  // SVG personalizzati basati sugli elementi del poster
  const icons = {
    leaf: <svg viewBox="0 0 24 24" fill="currentColor"><path d="M17,8C8,10 5.9,16.17 3.82,21.34L5.71,22L6.66,19.7C7.14,19.87 7.64,20 8,20C19,20 22,3 22,3C21,5 14,5.25 9,6.25C4,7.25 2,11.5 2,13.5C2,15.5 3.75,17.25 3.75,17.25C7,8 17,8 17,8Z" /></svg>,
    tree: <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12.66,2.77L12.66,2.77C12.29,2.42 11.71,2.42 11.34,2.77C8.78,5.15 6.5,8.56 6.5,11C6.5,13.28 7.97,15.22 9.97,16.06C10,16.07 11,21 11,21H13C13,21 13.97,16.05 14,16.05C16.03,15.19 17.5,13.25 17.5,11C17.5,8.56 15.22,5.15 12.66,2.77M6.91,4.73C7.28,5 7.2,5.13 7.2,6.5C5.15,8 4.33,8.26 3.06,8.94L2.58,10.37C4.05,11.18 4.22,11.33 5.5,13C5.5,13 4.76,15.13 4.76,15.13L6.91,16.9C8.06,15.83 8.93,15.31 9.8,14.95C9.34,13.8 9.04,13.36 8.66,12.6C7.42,10.96 6.91,9.08 6.91,4.73M17.09,4.73C17.09,9.08 16.58,10.96 15.34,12.6C14.96,13.36 14.66,13.8 14.2,14.95C15.07,15.31 15.94,15.83 17.09,16.9L19.24,15.13L18.5,13C19.78,11.33 19.96,11.18 21.42,10.37L20.94,8.94C19.68,8.26 18.86,8 16.8,6.5C16.8,5.13 16.72,5 17.09,4.73Z" /></svg>,
    plant: <svg viewBox="0 0 24 24" fill="currentColor"><path d="M15,8V4H19V8H15M3,18C3,20.21 4.79,22 7,22C9.21,22 11,20.21 11,18C11,15.79 9.21,13.86 7,13.86C4.79,13.86 3,15.79 3,18M11,13.27C12.32,13.91 13.29,15.29 13.29,17H15.5C15.5,15.07 14.3,13.24 13,12.4C13.22,11.28 13.82,10 14.5,9.67C15.21,9.32 16.68,9.57 16.92,11.07C17.13,12.25 16.33,13.03 15.3,13.07C15.05,13.07 14.71,12.94 14.5,12.82C14.35,12.95 14.18,13.11 14.04,13.29C14.82,13.73 15.5,13.47 16,13.37C17.41,13.03 18.56,11.47 18.15,9.83C17.76,8.37 16.35,7.62 14.61,8.07C13.12,8.47 12.03,10.15 11.68,11.38C10.91,11.03 10.07,10.86 9.22,10.86C8.94,10.86 8.67,10.93 8.39,10.97C8.4,10.41 8.5,9.89 8.65,9.43H5.04C5.18,9.85 5.27,10.32 5.28,10.84C4.95,10.97 4.61,11.15 4.3,11.34C4.14,10.5 4.32,9.3 4.78,8.74C5.47,7.88 7.13,8.1 7.5,8.84C7.75,9.36 7.25,9.83 7.1,9.9C6.95,9.97 7.3,10.58 7.72,10.49C8.3,10.37 9.16,9.36 8.66,8.11C8.17,6.9 6.22,6.36 4.88,7.42C3.61,8.43 3.37,10.28 3.72,11.91V11.94C2.5,12.96 1.72,14.47 1.72,16.18C1.72,19.18 4.03,21.5 7,21.5C10,21.5 12.28,19.18 12.28,16.18C12.28,15.03 11.83,13.92 11,13.27Z" /></svg>,
    water: <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12,20C8.69,20 6,17.31 6,14C6,10 12,3.25 12,3.25C12,3.25 18,10 18,14C18,17.31 15.31,20 12,20M12,2L5.75,9.74C5.27,10.33 5,11.16 5,12V13.25L5.75,14.25C6.33,15.23 7.28,15.96 8.5,16.25L9.25,15.25C9.75,14.47 10.67,14 11.67,14C12.67,14 13.58,14.47 14.08,15.25L14.83,16.25C16.05,15.96 17,15.23 17.58,14.25L18.33,13.25V12C18.33,11.16 18.05,10.33 17.58,9.74L11.33,2H12M12,5.84C11.17,7.08 10.33,8.5 9.58,9.8C9.08,10.67 8.57,11.6 8.14,12.41C7.87,12.93 7.64,13.41 7.44,13.83C7.47,13.47 7.5,13 7.53,12.5C7.61,11.23 7.62,9.35 7.66,7.35L8.94,5.53L8.97,5.5H9L11.17,8.14L11.94,9.08L12,9.14V7.5L12.47,5.84H12Z" /></svg>,
    sun: <svg viewBox="0 0 24 24" fill="currentColor"><path d="M3.55 19.09L4.96 20.5L6.76 18.71L5.34 17.29M12 6C8.69 6 6 8.69 6 12S8.69 18 12 18 18 15.31 18 12C18 8.68 15.31 6 12 6M20 13H23V11H20M17.24 18.71L19.04 20.5L20.45 19.09L18.66 17.29M20.45 5L19.04 3.6L17.24 5.39L18.66 6.81M13 1H11V4H13M6.76 5.39L4.96 3.6L3.55 5L5.34 6.81L6.76 5.39M1 13H4V11H1M13 20H11V23H13" /></svg>,
  };
  
  return (
    <div className={`${sizeClasses[size]} ${className}`}>
      {icons[name]}
    </div>
  );
}
```

## Stile per Grafici e Visualizzazioni

### Grafici con Stile Coordinato
```tsx
// components/ui/eco-stat.tsx
interface EcoStatProps {
  label: string;
  value: number;
  maxValue: number;
  unit?: string;
}

export function EcoStat({ label, value, maxValue, unit = '%' }: EcoStatProps) {
  const percentage = (value / maxValue) * 100;
  
  return (
    <div className="mb-6">
      <div className="flex justify-between mb-2">
        <span className="text-text-light text-sm">{label}</span>
        <span className="font-semibold">
          {value}{unit}
        </span>
      </div>
      <div className="h-3 bg-background-alt rounded-full overflow-hidden">
        <div 
          className="h-full bg-gradient-to-r from-accent to-primary rounded-full"
          style={{ width: `${percentage}%` }}
        />
      </div>
    </div>
  );
}
```

## Immagini e Pattern

Come ispirazione dal poster, consigliamo di utilizzare pattern e texture che ricordano la natura:

```tsx
// app/layout.tsx - esempio di background texture
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="it">
      <body className="bg-background bg-[url('/images/patterns/subtle-leaves.png')] bg-fixed">
        {children}
      </body>
    </html>
  );
}
``` 