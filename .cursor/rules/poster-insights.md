# Analisi del Poster Scientifico

## Elementi Chiave dal Poster

Dall'analisi dei file di riferimento nella cartella `samples`:

1. **Layout e Struttura**
   - Organizzazione a blocchi ben definiti
   - Gerarchia visiva chiara con informazioni principali in alto
   - Uso di separatori curvilinei che creano un senso di fluidità
   - Arrotondamento dei bordi di ogni sezione per un aspetto organico

2. **Palette Colori**
   - **Predominanza di verdi** in diverse tonalità
   - Sfumature graduali che creano profondità
   - Contrasto tra testo scuro e sfondi chiari per leggibilità
   - Uso di overlay trasparenti per creare stratificazione

3. **Elementi Grafici**
   - **Icone e simboli** legati alla natura (foglie, alberi, piante)
   - **Onde e forme organiche** che separano le sezioni
   - **Pattern di foglie** come texture di sfondo in alcune aree
   - **Effetti di ombreggiatura** per dare profondità ai box

4. **Tipografia**
   - **Titoli grandi e bold** per i punti principali
   - Font sans-serif moderni per tutto il testo
   - Ottimo contrasto tra dimensioni per la gerarchia informativa
   - Uso del colore per distinguere i livelli di importanza

## Conversione dal Poster al Web

### Adattamento Responsive
Come trasformare il layout fisso del poster in un design web responsive:

1. **Da fisso a fluido**
   - Convertire le misure fisse in unità relative (%, rem, vh/vw)
   - Mantenere le proporzioni degli elementi nei vari breakpoint
   - Garantire che le forme organiche si adattino ai diversi formati schermo

2. **Cambio di orientamento**
   - Su desktop: layout simile al poster, con colonne affiancate
   - Su mobile: trasformazione in layout a singola colonna
   - Mantenimento della gerarchia visiva in entrambe le modalità

### Componenti Principali da Replicare

1. **Header con stile "natura"**
   ```tsx
   // Esempio reinterpretazione dell'intestazione del poster
   <div className="relative overflow-hidden rounded-b-3xl bg-gradient-to-b from-primary-dark via-primary to-primary-light">
     {/* Pattern overlay */}
     <div className="absolute inset-0 opacity-15">
       <Image 
         src="/images/patterns/leaf-pattern.png" 
         alt="" 
         fill 
         className="object-cover mix-blend-overlay"
         aria-hidden="true"
       />
     </div>
     
     <div className="relative z-10 py-20 px-6 text-center">
       <h1 className="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-4">
         Radici di Libertà
       </h1>
       <p className="text-lg md:text-xl lg:text-2xl text-white/90 max-w-2xl mx-auto">
         Rigenerare possibilità e benessere attraverso la natura
       </p>
     </div>
     
     {/* Curva organica inferiore - simile al poster */}
     <div className="absolute bottom-0 left-0 w-full h-16">
       <svg viewBox="0 0 1200 120" preserveAspectRatio="none" className="w-full h-full">
         <path 
           fill="var(--color-background)" 
           d="M0,0V46.29c47.79,22.2,103.59,32.17,158,28,70.36-5.37,136.33-33.31,206.8-37.5C438.64,32.43,512.34,53.67,583,72.05c69.27,18,138.3,24.88,209.4,13.08,36.15-6,69.85-17.84,104.45-29.34C989.49,25,1113-14.29,1200,52.47V0Z"
           opacity=".25"
         ></path>
         <path 
           fill="var(--color-background)" 
           d="M0,0V15.81C13,36.92,27.64,56.86,47.69,72.05,99.41,111.27,165,111,224.58,91.58c31.15-10.15,60.09-26.07,89.67-39.8,40.92-19,84.73-46,130.83-49.67,36.26-2.85,70.9,9.42,98.6,31.56,31.77,25.39,62.32,62,103.63,73,40.44,10.79,81.35-6.69,119.13-24.28s75.16-39,116.92-43.05c59.73-5.85,113.28,22.88,168.9,38.84,30.2,8.66,59,6.17,87.09-7.5,22.43-10.89,48-26.93,60.65-49.24V0Z"
           opacity=".5"
         ></path>
         <path 
           fill="var(--color-background)" 
           d="M0,0V5.63C149.93,59,314.09,71.32,475.83,42.57c43-7.64,84.23-20.12,127.61-26.46,59-8.63,112.48,12.24,165.56,35.4C827.93,77.22,886,95.24,951.2,90c86.53-7,172.46-45.71,248.8-84.81V0Z"
         ></path>
       </svg>
     </div>
   </div>
   ```

2. **Box tematici con stile del poster**
   ```tsx
   // Card design ispirata al poster
   <div className="rounded-3xl overflow-hidden shadow-lg">
     {/* Header colorato come nel poster */}
     <div className="bg-gradient-to-r from-primary to-primary-dark px-6 py-4 text-white">
       <h3 className="text-xl font-bold">Obiettivi</h3>
     </div>
     
     {/* Contenuto con sfondo chiaro */}
     <div className="bg-background p-6">
       <ul className="space-y-3">
         {objectives.map((objective, index) => (
           <li key={index} className="flex items-start gap-3">
             <span className="text-primary mt-1">
               <EcoIcon name="leaf" size="sm" />
             </span>
             <span>{objective}</span>
           </li>
         ))}
       </ul>
     </div>
   </div>
   ```

3. **Visualizzazione dati in stile poster**
   ```tsx
   // Stile grafico simile alle visualizzazioni del poster
   <div className="bg-white rounded-3xl shadow-md p-6">
     <h3 className="text-xl font-semibold text-primary mb-6">Indicatori di Benessere</h3>
     
     <div className="space-y-6">
       <div className="relative">
         <div className="flex justify-between mb-2">
           <span>Riduzione dello stress</span>
           <span className="font-semibold">67%</span>
         </div>
         <div className="h-2.5 bg-gray-100 rounded-full">
           <div className="h-2.5 rounded-full bg-gradient-to-r from-accent to-primary" style={{width: '67%'}}></div>
         </div>
       </div>
       
       {/* Altri indicatori... */}
     </div>
   </div>
   ```

## Ottimizzazione delle Immagini

Per riprodurre l'aspetto del poster, è importante avere:

1. **Estrazione degli elementi grafici**
   - Ottenere versioni vettoriali delle icone e simboli (SVG)
   - Isolare le curve e forme organiche per riutilizzarle come divisori
   - Catturare le texture e pattern per gli sfondi

2. **Trattamento delle immagini**
   - Compressione ottimizzata per il web
   - Generazione di versioni responsive per diversi dispositivi
   - Conversione in formati moderni (WebP) mantenendo fallback

3. **Icone e simboli personalizzati**
   - Ricalcare le icone uniche del poster come componenti SVG
   - Mantenere coerenza nella dimensione e nello stile
   - Garantire accessibilità con colori high-contrast se necessario

## Esempi di Implementazione

### Sfondo con Pattern di Foglie
```css
/* Esempio di texture leggera ispirata al poster */
.leaf-texture-bg {
  background-color: var(--color-background);
  background-image: url('/images/patterns/leaf-pattern-light.png');
  background-size: 300px;
  background-repeat: repeat;
  background-blend-mode: soft-light;
  background-attachment: fixed;
}
```

### Separatore d'Onda
```tsx
// Separatore curvo come nel poster
export function WaveDivider({ 
  color = 'var(--color-background)',
  className = ''
}) {
  return (
    <div className={`w-full h-24 overflow-hidden ${className}`}>
      <svg viewBox="0 0 1200 120" preserveAspectRatio="none" className="w-full h-full">
        <path 
          fill={color} 
          d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V120H0V95.8C59.71,118.92,146.5,85.03,216.23,70.28,289.62,55.07,262.41,67.23,321.39,56.44Z"
        />
      </svg>
    </div>
  );
}
```

### Box Organico
```tsx
// Box con forma organica simile al poster
export function OrganicBox({ children, className = '' }) {
  return (
    <div className={`relative rounded-3xl overflow-hidden ${className}`}>
      {/* Forma organica decorativa */}
      <div className="absolute top-0 right-0 w-64 h-64 -translate-y-1/3 translate-x-1/3">
        <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg" className="w-full h-full opacity-10">
          <path fill="currentColor" d="M47.7,-73.2C59.5,-65.3,65.2,-48.3,71.3,-32.5C77.5,-16.6,84.2,-2,83.1,12.2C82,26.3,73.2,40,61.3,49C49.5,58,34.7,62.3,19.7,67.4C4.8,72.4,-10.2,78.3,-24.3,76.4C-38.3,74.5,-51.4,64.9,-60.2,52.5C-69.1,40,-73.6,24.7,-73.7,10.2C-73.8,-4.3,-69.5,-17.9,-64.2,-32.6C-58.9,-47.3,-52.5,-63.1,-41.2,-70.7C-29.9,-78.3,-14.9,-77.6,1.3,-79.6C17.6,-81.6,35.8,-81.2,47.7,-73.2Z" transform="translate(100 100)" />
        </svg>
      </div>
      
      {/* Contenuto effettivo */}
      <div className="relative z-10">
        {children}
      </div>
    </div>
  );
}
``` 