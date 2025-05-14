# Riferimenti al Design del Poster Scientifico

## Integrazione del Poster nel Design Web

Il poster scientifico presente nei file di riferimento (`samples/Poster Scientifico - Lab. Ambiente Naturale e Benessere.png` e `samples/WEB - Poster Scientifico - Lab. Ambiente Naturale e Benessere.pdf`) costituisce un importante riferimento visivo per il sito web. Dovremo mantenere coerenza con questi elementi grafici.

## Elementi da Riprendere dal Poster

### Stile Visivo
- Forme arrotondate e organiche che richiamano la natura
- Utilizzo di elementi grafici come foglie, alberi e piante
- Layout pulito con spazi ben definiti
- Schema a blocchi per la separazione dei contenuti

### Sfondi e Texture
- Sfondi sfumati verdi nelle diverse sezioni
- Possibili texture leggere che richiamano elementi naturali
- Utilizzo di separatori curvilinei tra le sezioni

### Elementi Grafici
- Icone di piante/foglie per rappresentare i punti elenco
- Utilizzo di grafici e visualizzazioni per rappresentare dati
- Immagini di natura e attività di giardinaggio

### Header
- Riadattare il titolo principale del poster come hero section
- Utilizzare font e dimensioni simili per mantenere riconoscibilità

## Implementazione Tecnica

### Componenti CSS Custom
```css
/* Stili ispirati al design del poster */
.poster-section {
  border-radius: 2rem;
  background: linear-gradient(145deg, var(--color-accent-light), var(--color-primary));
  padding: 2rem;
  margin-bottom: 2rem;
}

.leaf-bullet-list li {
  list-style-type: none;
  position: relative;
  padding-left: 1.5rem;
}

.leaf-bullet-list li::before {
  content: "🍃"; /* Sostituire con SVG personalizzata */
  position: absolute;
  left: 0;
  color: var(--color-accent);
}

.wave-divider {
  height: 5rem;
  background-image: url('/images/wave-divider.svg');
  background-repeat: no-repeat;
  background-size: cover;
  margin: 2rem 0;
}
```

### SVG per Decorazioni
Creare SVG personalizzati basati sugli elementi grafici del poster:
- Wave divider (separatore ondulato tra sezioni)
- Foglie e piante per bullet points
- Bordi curvilinei per le cards

### Strategie di Implementazione
1. **Estrarre i colori esatti** dal poster per affinarli nella tavolozza
2. **Fotografare o vettorializzare** gli elementi grafici principali
3. **Riprodurre i layout** mantenendo le proporzioni delle sezioni
4. **Adattare in modo responsivo** gli elementi del poster fisso per il web

## Adattamento al Web

### Desktop vs Mobile
- Su desktop: layout simile al poster con sezioni affiancate dove appropriato
- Su mobile: riorganizzazione in colonna mantenendo gli stessi elementi visivi

### Interattività
- Aggiungere animazioni subtili agli elementi statici del poster
- Transizioni tra sezioni che mantengano il senso di fluidità
- Effetti hover che esaltino gli elementi grafici

## Immagini di Riferimento

Posizionamento di riferimenti al poster originale nella cartella:

```
public/
├── images/
│   ├── design-references/
│   │   ├── poster-full.jpg       # Poster intero (compresso)
│   │   ├── poster-section-1.jpg  # Header section
│   │   ├── poster-section-2.jpg  # Problem section
│   │   └── poster-elements/      # Elementi grafici estratti
``` 