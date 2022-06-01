# Calcolatori (Teoria)

## Toolchain

Ovvero il processo di generazione del linguaggio macchina. La conversione è effettuata dal **compilatore**.

1. **Preprocessore**: gestisce le direttive `#`, in pratica sostituisce pezzi di codice.
2. **Compilatore**: passa da C a Assembly (`.s`)
3. **Assembler**: passa da Assembly a linguaggio macchina (`.o`)
4. **Linker**: mette assieme codice in linguaggio macchina e librerie per generare un eseguibile

Di tutto questo si occupa un _driver_ el'eseguibile può essere caricato tramite la system call _exec()_

`gcc` invoca:

1. cpp
2. cc: conosce l'architettura target - possibili ottimizzazioni
3. as
4. ld

## Assembler

L'**assembler** si occupa anche di altre cose:

- convertire istruzioni/numeri (pseudo istruzioni come `mv` e `j`)
- gestire label e salti
- generare meta-dati

## File Oggetto

È composto da:

- **Header**: dimensione e posizione degli altri segmenti del file
- **Segmenti**:
  - **di Testo**: contiene il codice in linguaggio macchina
  - **dati statici**: contiene i dati allocati per la durata del programma
- **Tabella dei simboli**:
  - Associa simboli a indirizzi
  - Enumera simboli non definiti
- **Tabella di rilocazione**:
  - Enumera istruzioni da _patchare_ (indirizzi assoluti)

## Linker

Mette assieme uno o più file oggetto eseguendo le rilocazioni. Praticamente elimina lee tabelle dei simboli e di rilocazione mettendo assieme tutto quello che ha a disposizione.

### Tipi di Simboli

- definiti: associati a un indirizzo relativo
- non definiti: usati in un file ma definiti in uno diverso
- locali: definiti e usati in un file ma non usabili in un altro file

In ogni caso a ogni simbolo viene associato un indirizzo assoluto.

### Linking phase

1. Dispone i segmenti in memoria
2. Assegna un indirizzo assoluto a ogni simbolo
3. Corregge le varie istruzioni con indirizzi calcolati
4. Incapsulamento nell'eseguibile

### Librerie

Ovvero collezioni di file `.o`

- **Librerie statiche `.o`**: collezioni di file oggetto, ld fa tutto il lavoro (ma occhio alle dimensioni dell'eseguibile)
- **Librerie dinamiche `.so`**: il linking avviene a tempo di esecuzione
  - usa riferimenti a librerie ma non le include, ogni eseguibile hah infatti un _linker dinamico_

#### Lazy linking

Il linking non viene fatto durante il caricamento ma in maniera dinamica a runtime. Viene in fatti chiamato uno **stub** che si occupa di caricamento, rilocazione e linking

## Il Processore

### Concetti di reti logiche

**rete logica combinatoria**: circuito composto da porte logiche che produce un output statico dell'input

**elementi di stato o sequenziali**: perché l'uscita a un ingresso dipende anche dagli ingressi precedenti

![Tabella di Controllo ALU](images/TabellaControlloALU.png)

![CPU](images/CPU.png)

## La Pipeline

Chiaramente non si spreca tempo con una sola istruzione per tutti i passaggi. Qui entra in gioco la **pipeline**

A dettare il periodo di clock sono ovviamente le istruzioni più lente.

**Vantaggi del RISC**:

- Istruzioni della stessa lunghezza
- Codici operandi in posizioni fisse
- Si può usare la alu per il calcolo degli indirizzi (accesso in memoria solo a ld/st)
- Gli accessi avvengono in un solo stadio della pipeline

### ⚠️ HAZARD

#### Hazard Strutturali

Causati dall'architettura, ad esempio non posso caricare istruzioni e memorizzare operandi nello steso ciclo

#### Hazard sui dati

Quando la pipeline è in stallo in attesa di informazioni di stadi precedenti. Si può vedere quando due istruzioni usano lo stesso registro e sono vicine. Per risolvere basta scambiare le posizioni delle istruzioni ottimizzando la pipeline.

_continua..._
