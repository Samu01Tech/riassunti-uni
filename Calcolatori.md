# Calcolatori (Assembly)

---

- [Calcolatori (Assembly)](#calcolatori-assembly)
  - [Cos'è?](#cosè)
  - [ISA](#isa)
  - [Procedimento](#procedimento)
  - [Registri](#registri)
  - [Istruzioni](#istruzioni)
  - [RISC vs CISC](#risc-vs-cisc)
  - [Istruzioni condizionate](#istruzioni-condizionate)
  - [RISC sample](#risc-sample)
  - [Accesso alla memoria](#accesso-alla-memoria)
  - [ISA vs ABI](#isa-vs-abi)
- [RISC-V](#risc-v)
  - [Cenni storici](#cenni-storici)
  - [Operazioni Aritmetiche](#operazioni-aritmetiche)
  - [I registri](#i-registri)
  - [Accesso alla memoria](#accesso-alla-memoria-1)
  - [Operandi immediati](#operandi-immediati)
  - [Costante 0](#costante-0)
  - [Codifica esadecimale](#codifica-esadecimale)
  - [Codifica in codice macchina](#codifica-in-codice-macchina)
  - [Istruzioni di tipo I](#istruzioni-di-tipo-i)
  - [Key Letters Istruzioni](#key-letters-istruzioni)
  - [Operazioni Logiche](#operazioni-logiche)
    - [Shift Logico](#shift-logico)
    - [AND `and`](#and-and)
    - [OR `or`](#or-or)
    - [OR esclusivo `xor`](#or-esclusivo-xor)
    - [NOT](#not)
  - [Istruzioni per prendere decisioni](#istruzioni-per-prendere-decisioni)
    - [Il costrutto case/switch](#il-costrutto-caseswitch)
  - [Procedure](#procedure)
    - [Stack](#stack)
    - [Storage class](#storage-class)
    - [Record di Attivazione](#record-di-attivazione)
- [Assembly INTEL](#assembly-intel)
  - [I registri](#i-registri-1)
  - [Convenzioni di Chiamata (Non dell'architettura)](#convenzioni-di-chiamata-non-dellarchitettura)
  - [Indirizzamento](#indirizzamento)
  - [Key letters/word](#key-lettersword)
  - [Istruzioni](#istruzioni-1)
- [Assembly ARM](#assembly-arm)
  - [Registri](#registri-1)
    - [Flag Register](#flag-register)
  - [Key letters/word](#key-lettersword-1)
  - [Convenzioni di chiamata](#convenzioni-di-chiamata)
  - [Indirizzamento](#indirizzamento-1)
  - [Operazioni Aritmetiche e Logiche](#operazioni-aritmetiche-e-logiche)

---

## Cos'è?

Rappresenta attraverso codici mnemonici sequenze di 0 e 1 che permettono di eseguire operazioni logiche e aritmetiche.

Un programma Assembly è un file ASCII che contengono una descrizione testuale delle operazioni. Assembly deve essere compilato da un **Assembler** che traduce in linguaggio macchina.

Ad ogni istruzione Assembly corrisponde un'istruzione in linguaggio macchina.

## ISA

**Instruction Set Architecture**: insieme delle sequenze di bit riconosciute da una CPU. L'ISA di una CPU ne definisce anche il linguaggio Assembly.

## Procedimento

1. **Fetch**: preleva le istruzioni dalla memoria
2. **Decode**: decodifica l'istruzione
3. **Execute**: esegue l'istruzione

Assembly è prevalentemente **sequenziale** ma esistono istruzioni di **salto** condizionale.

## Registri

I dati su cui opera Assembly possono essere:

- **immediati** o **costanti**
- Contenuti in **registri**
- Contenuti in **memoria**

Registro _k_ bit = _k_ flip-flop D

I registri possono essere:

- **general** purpose
- **special** purpose

## Istruzioni

- Aritmetico/logiche
- Movimento dati
- Controllo di flusso (salti)

## RISC vs CISC

- RISC: Reduced Instruction Set Computer - semplifica l'implementazione della CPU
  - più semplice e regolare
  - no operandi o destinazione in memoria
  - si accede alla memoria con _load_ e _store_
- CISC: Complex Instruction Set Computer - semplifica la scrittura di programmi Assembly
  - maggior numero di istruzioni più potenti
  - opera anche in memoria

## Istruzioni condizionate

Attraverso **flag** contenuti in registri speciali che vengono settati.

## RISC sample

```
<opcode> <dst (reg)>, <arg1 (reg)>, <arg2 (reg o immediato)>

load <reg>, <memory location>
store <memory location>, <store>
```

## Accesso alla memoria

1. Indirizzo di memoria costante come valore immediato
2. Indirizzo contenuto in un registro
3. Indirizzo ottenuto shiftando un valore in un registro
4. Combinazione

5. :x: Assoluto: codificato in una istruzione Assembly
6. Indiretto: per i puntatori
7. Base + Spiazzamento (reg + valore immediato)
8. Base + Indice (reg + reg[shiftato])
9. Base + Indice + Spiazzamento (reg + reg[shiftato] + valore immediato)

## ISA vs ABI

- **ISA**: definisce le istruzioni riconosciute dalla CPU ed i registri
- **ABI**: Application Binary Interface - è un'insieme di convenzioni software che indicano come usare i registri (es. convenzioni di chiamata)

**Convenzioni**:

- Come / dove passare i parametri: stack o registri?
- Quali registri preservare?
- Quando un programma invoca una subroutine, quali registri
  conterranno un certo valore al ritorno dalla subroutine

# RISC-V

Il "linguaggio" di un computer si compone di un vocabolario di istruzioni detto **Instruction Set**

Ogni processore ha il suo instruction set.

**Von Neumann**

- Semplicità dei dispositivi richiesti
- Chiarezza delle applicazioni
- Velocità di Esecuzione

## Cenni storici

Nasce nell'università did Berkeley nel 2010.
È open source e moderna, usata in certe applicazioni specifiche.

## Operazioni Aritmetiche

È naturale che l'architettura RISC-V supporti le operazioni aritmetiche.

```s
add a, b, c
sub d, a, e

# questo un commento
# l'operando destinatario è sempre il primo
```

## I registri

Il RISC-V contiene 32 registri a 64bit.

- 64bit = _double word_
- 32bit = _word_

```s
add x5, x20, x21
```

## Accesso alla memoria

Ovviamente i registri non bastano per effettuare tutti i calcoli. È necessario ricorrere alla memoria.

La memoria è una sequenza di bit organizzata in gruppi di 8bit.

Non si accede quasi mai, per quanto possibile, al singolo byte. Si sfruttano _word 32b_ e _double word 64b_.

In RISC-V per caricare in memoria un valore bisogna specificare l'indirizzo.

Esso è specificato tramite **base** (reg) + **offset** (const)

```s
# carica in x9 il valore di che ha indirizzo x22 + 8 * 8 (ottava parola doppia)
ld x9, 64(x22)

add x9, x21, x9 # x9 = x9 + x21
sd x9, 96(x22) # salva x9 in memoria a x22 + 12*8
```

**Register Spilling**: normalmente si richiederebbe di caricare e scaricare in memoria variabili in base a se ne si fa uso. Questa operazione è eseguita dal compilatore che stima il _working set_ e mette le operazioni appropriate.

## Operandi immediati

Rendono più veloci le situazioni più comuni (ex. caricare una costante per poi fare operazioni)

```s
addi x22, x22, 4
```

## Costante 0

La costante 0 è contenuta nel registro `x0`.

## Codifica esadecimale

Gruppi di 4 bit che rappresentano un numero da 0 a 16.

`1001 1101` = `0x9D`

- **Little Endian**
  - Byte più significativo più a sinistra
  - Intel e RISC-V
  - `0xEA01BD1C` -> `EA` = addr 3, `01` = addr 2, `BD` = addr 1, `1C` = addr 0
- **Big Endian**
  - Byte più significativo più a destra
  - Protocolli Internet

## Codifica in codice macchina

Ogni istruzione, in RISC-V, viene codificata in 32 bit.
`add x9, x20, x21`

```
0000000 10101 10100 000 01001 0110011
7bit - 5bit - 5bit - 3bit - 5bit - 7bit
funz7 - rs2 - rs1 - funz3 - rd - codeop
```

Siccome RISC-V ha 32 registri posso rappresentarli con 5bit (0-31).

## Istruzioni di tipo I

Usato per casi di indirizzamento immediato o uso di costanti.

```
12bit - 5bit - 3bit - 5bit - 7bit
costante/indirizzo - rs1 - funz3 - rd - codop
```

## Key Letters Istruzioni

- `i`: immmediato - costante
- `d`: _double word_
- `w`: _word_
- `h`: _half word_
- `b`: _byte_
- `u`: _unsigned_

## Operazioni Logiche

### Shift Logico

**A sinistra**: Inserisce degli zeri nella posizione meno significativa.

```s
slli x11, x19, 4
```

Ovvero moltiplica l'operando per $2^k$

**Problema**: in caso di numeri negativi questa operazione non è sempre corretta. (Finché rimane nel range di rappresentabilità)

**A destra**: Inserisce dei valori nella posizione più significativa. L'effetto è una divisione per $2^k$.

**Problema**: in caso di numeri negativi questa operazione non sarebbe corretta se inserissimo degli 0.

Per questo motivo esiste lo **shift aritmetico** che inserisce bit uguali al segno e non 0.

```s
slli x11, x19, 4
srli x11, x19, 4
srai x11, x19, 4

# possibile anche senza i
```

### AND `and`

Forza alcuni bit a 0. Solo se entrambi 1.

### OR `or`

Forza alcuni bit a 1 secondo una maschera con 1 in posizione corrispondente.

es. rotazione di un numero

### OR esclusivo `xor`

Produce 1 se i due operandi sono diversi.

Utile per annullare un registro

```s
xor, x9, x9, x9
```

### NOT

In RISC-V non è presente un operatore NOT. Tuttavia si può usare:

```s
xor x9, x9, x10

# con x10 tutti 1
```

## Istruzioni per prendere decisioni

Il linguaggio macchina fornisce istruzioni di salto condizionato.

```s
beq rs1, rs2, L1 # se rs1 == rs2 allora salta all'etichetta L1

bne rs1, rs2, L1 # se rs1 != rs2 allora salta all'etichetta L1
```

Le LABEL vengono tradotte in indirizzi.

Questa struttura può essere usata anche per creare dei cicli.

**Blocchi di Base**: sequenza di istruzioni tar due salti condizionati (conditional branch).

Altri confronti possono essere:

- `blt` - lower than
- `bgt` - greater than
- `bltu` - lower than unsigned
- `bgeu` - greater equal than unsigned

**Controllare se un indice è fuori da un array**

```s
bgeu x20, x11, FuotiLimite # se x20 >= x11 allora salta all'etichetta FuotiLimite
```

### Il costrutto case/switch

È possibile memorizzare i vari indirizzi del codice da eseguire in una tabella (sequenza di word). Si carica in unu registro l'indirizzo a cui saltare. Si salta all'indirizzo puntato da registro tramite `jalr` (jump and link register).

## Procedure

Una procedura può essere paragonata a una funzione, si può pensare a una scatola nera che esegue un certo task ma della quale non conosciamo i dettagli.

È importante specificare il protocollo (o convenzione) di chiamata della procedura.

1. Caricare i parametri
2. Trasferire il controllo alla procedura
   1. Acquisire le risorse necessarie
   2. Eseguire
   3. Caricare i valori di ritorno
   4. Restituire il controllo al chiamante
3. Prendere i valori di ritorno e ripulire i registri

**Convenzioni RISC-V**

- `x10 - x17`: parametri di ingresso/valori di ritorno
- `x1`: indirizzo di ritorno (return address)
  - `jal e jalr` memorizzano in automatico in x1 l'indirizzo di ritorno
  - In `x1` viene salvato il PC + 4 (program counter + 4) (istruzione successiva) e poi va alla posizione specificata
  - A fine procedura basta fare `jalr x0, 0(x1)`

### Stack

In certi casi i registri non bastano. Si utilizza una struttura a stack LIFO in cui si può caricare parametri extra, a partire da `x2` anche detto **stack pointer**.

1. Prologo

   1. Il compilatore scegli l'etichetta per la procedura
   2. Salvataggio di tutti i registri da usare
   3. Possibile uso stack

2. Esecuzione

```s
addi sp, sp, -24 # alloco spazio per 24 byte (3 long long int)
sd x5, 16(sp) # salvo x5 in sp+16
sd x6, 8(sp) # salvo x6 in sp+8
sd x20, 0(sp) # salvo x20 in sp

# ... operazioni
```

3. Epilogo

```s
addi x10, x20, 0 # prendo il valore di ritorno
ld x20, 0(sp) # ripristino i registri
ld x6, 8(sp) # ripristino i registri
ld x5, 16(sp) # ripristino i registri
addi sp, sp, 24 # libero spazio nello stack
jalr x0, 0(x1) # torno al chiamante
```

**Ottimizzazioni**
`x5` e `x6` sono usati solo per il prologo. Non devono essere salvati durante la chiamata.

**Convenzioni**

- `x5-x7 e x28-x31`: registri temporanei, non salvati in caso di chiamata a procedura
- `x8-x9 e x18-x27`: registri da salvare

_Esempio Fattoriale_

```cpp
long long int fact(long long int n) {
    if (n < 1)
        return 1;
    else
        return n*fact(n-1);
}
```

Andremo a salvaguardare x1 e x10 nello stack.

```s
fact:
    addi sp, sp, 16 # alloco spazio per 16 byte (2 long long int)
    sd x1, 8(sp) # salvo x1 in sp+8
    sd x10, 0(sp) # salvo x10 in sp
    # testiamo se n < 1
    addi x5, x10, -1 # x5 = n-1
    bge x5, x0, L1 # se n >= 1 allora salta all'etichetta L1
    addi x10, x0, 1 # x10 = 1
    addi sp, sp, 16 # libero spazio nello stack
    jalr x0, 0(x1) # torno al chiamante
L1:
    addi x10, x10, 1 # x10 = n*(n-1)
    jal x1, fact # chiamo la procedura fact
    addi x6, x10, 0 # x6 = ritorno della procedura
    ld x10, 0(sp) # ripristino x10
    ld x1, 8(sp) # ripristino x1
    addi sp, sp, 16 # libero spazio nello stack
    mul x10, x10, x6 # x10 = n*(n-1)*ritorno della procedura
    jalr x0, 0(x1) # torno al chiamante
```

### Storage class

Le variabili in C sono definite per:

- tipo
- storage class

Storage class:

- automatica: variabile che viene allocata automaticamente all'inizio della funzione
- statica: variabile che viene allocata all'inizio del programma (globale)

Le variabili globali sono memorizzate in una zona di memoria specifica: il registro `x3` o `gp` (global pointer).

### Record di Attivazione

Il segmento di stack che contiene registri salvati e variabili locali relative a una funzione è chiamato **record di attivazione**.

Esiste il **frame pointer** che punta al top dello stack.

# Assembly INTEL

È una architettura di tipo CISC (Complex Instruction Set Computer).

Ha un gran numero di istruzioni e molte modalità ddi indirizzamento.

## I registri

I registri, 16 da 64 bit general purpose, nell'architettura INTEL sono preceduti dal prefisso `%` e sono:

| Registro       | Descrizione                                         |
| -------------- | --------------------------------------------------- |
| `%rax`         | registro di tipo rax (general purpose)              |
| `%rbx`         | registro di tipo rbx (general purpose)              |
| `%rcx`         | registro di tipo rcx (general purpose)              |
| `%rdx`         | registro di tipo rdx (general purpose)              |
| `%r8` - `%r15` | registri di tipo r8-r15 (general purpose)           |
| `%rbp`         | registro base pointer (puntatore a stack frame)     |
| `%rsp`         | registro stack pointer (puntatore allo stack)       |
| `%rsi`         | registri obsoleti per copia array source index      |
| `%rdi`         | registri obsoleti per copia array destination index |

- `%rax`: 64bit
- `%eax`: 32 bit meno significativi
- `%ax`: 16 bit meno significativi
- `%al`: 8 bit alti (solo registri a - d)
- `%ah`: 8 bit bassi

**Registri Speciali**

- `%rip`: Instruction Point Visible (indica l'indirizzo dell'istruzione corrente)
- `%rflags` -> `%eflags` -> `%flags`: Flag Register (contiene le informazioni di stato del processore)
  - CF: Carry Flag - se unsigned interger overflow o carry-out
  - ZF: Zero Flag - se risultato è zero
  - SF: Sign Flag - se risultato è negativo
  - OF: Overflow Flag - se risultato è maggiore di `2^64` overflow
  - IF: Interrupt Flag - se è stato generato un'interruzione

## Convenzioni di Chiamata (Non dell'architettura)

- **Argomenti**: di, si, dx, cx, 8, 9. Il resto sullo stack
- **Valori di ritorno**: ax, dx
- **Registri preservati**: bp, bx, 12, 13, 14, 15
- **Registri temporanei**: ax, r10, r11 + passaggio di parametri

## Indirizzamento

Le istruzioni sono prevalentemente a due operandi, in quanto il secondo è implicito.

- **Sorgente**:
  - Immediato `$`
  - Registro `%`
  - Memoria `0x`
- **Destinazione**:
  - Registro `%`
  - Memoria `0x`

Esiste quindi la scrittura diretta in memoria. **Non possono essere entrambi sulla memoria**.

```
<displacement> (<base reg>, <index reg>, <scale>)

    displacement: valore di offset
    base reg: registro di base
    index reg: registro di indice
    scale: fattore di scala

<displacement> + <base reg> + <index reg> * <scale>
```

È necessario solo indicare il registro di base. Gli altri possono essere omessi.

## Key letters/word

- `b`: 8bit
- `w`: 16bit
- `l`: 32bit
- `q`: 64bit
- `%`: registro
- `$`: costante
- `429`: indirizzo costante

## Istruzioni

```s
mov <src>, <dst> # copia da sorgente a destinazione
  movsx <src>, <dst> # copia con segno
  movzx <src>, <dst> # copia con 0

add / adc # add / add with carry
sub / mul / div / inc / dec # subtract / multiply / divide / increment / decrement

# rotation, shift, boolean, neg

push %reg # push onto stack
  (subq + movq)
pop %reg # pop from stack
  (movq + addq)

cmp arg1, arg2 # compare
# esegue arg2 - arg1 e setta i flag di stato, risultato non memorizzato

test arg1, arg2 # test
# esegue arg2 & arg1 e setta i flag di stato, risultato non memorizzato
# usato per verificare se il valore è 0 o negativo

jmp <label> # jump incondizionato

je, jnz, jc, jnc # salti condizionati

call <label> # call procedure
  # push sullo stack della prossima istruzione, modifica PC alla procedura, subq + movq

ret # return from procedure
  # pop dallo stack (%rip), modifica PC al chiamante, movq + addq

lea <src>, <dst> # load effective address
# per calcolare indirizzi senza fare accessi,
```

# Assembly ARM

È un'architettura RISC (Reduced Instruction Set Computer).

Offre tante modalità di indirizzamento, più semplice, obiettivo del risparmio energetico.

## Registri

Fornisce 16 registri a 32 bit, general purpose; con nomi da `r0` a `r15`.

- `r13` == `sp`: stack pointer
- `r14` == `lr`: link register
- `r15` == `pc`: program counter

`Application Program Status Register` (`APSR`) / `Current Program Status Register` (`CPSR`) -> **Flag Register**

### Flag Register

- `eq`: equal
- `ne`: not equal
- `hs`: higher same | `cs`: carry set
- `lo`: lower same | `cc`: carry clear
- `mi`: minus - se operazione precedente era negativa
- `pl`: plus - se operazione precedente era positiva
- `vs`: overflow - se operazione precedente era maggiore di `2^64`
- `vc`: no overflow - se operazione precedente era minore di `2^64`
- `hi`: higher - se operazione precedente era maggiore di argomento
- `ls`: lower - se operazione precedente era minore di argomento
- `ge`, `lt`, `gt`, `le`: greater, less, greater than, less than

## Key letters/word

- `#`: costante
- `r`: 32bit
- `h`: 16bit
- `b`: 8bit

## Convenzioni di chiamata

- `r0`-`r3`: **argomenti**, gli altri sullo stack
- `r4`-`r11`: **registri preservati**
- `r0`, `r1`: Valori di **ritorno**

## Indirizzamento

- Istruzioni prevalentemente a 3 argomenti
- Operando sinistro: registro
- Operando destro: immediato o registro

**Per accedere in memoria:**

- `ldr` e `str` -> **load/store**
- `ldm` e `stm` -> **load/store multiple**

```
i = <base> + {<offset> | <indice (shiftato)>}
```

```s
ldr r0, [r1] # load from memory
ldr r0, [r1, #4] # load from memory with offset r1 + 4
ldr r0, [r1, r2] # load from memory with index r1 + r2
ldr r0, [r1 + r2, lsl #2] # load from memory with index and shift r1 + r2 << 8


# pre-indexed
ldr r0, [r1, #4]
  r0 = mem[r1 + 4]
  r1 = non modificato

#pre-indexed writeback
ldr r0, [r1, #4]!
  r0 = mem[r1 + 4]
  r1 = r1 + 4

#pre-indexed shifted
ldr r0, [r1, r2, lsl #4]
  r0 = mem[r1 + r2 << 4]
  r1 = non modificato

#pre-indexed shifted writeback
ldr r0, [r1, r2, lsl #4]!
  r0 = mem[r1 + r2 << 4]
  r1 = r1 + r2 << 4

#post-indexed
ldr r0, [r1], #4
  r0 = mem[r1]
  r1 = r1 + 4

#post-indexed writeback
ldr r0, [r1], r2, lsl #4
  r0 = mem[r1]
  r1 = r1 + r2 << 4
```

## Operazioni Aritmetiche e Logiche

```
<opcode>[condition][s] rd, rl, <r>
```

```assembly
add r0, r1, r2 # add
adds r0, r1, r2 # add with sign
addc r0, r1, r2 # add with carry
sub r0, r1, r2 # subtract / subtract with carry r1- r2
rsb r0, r1, r2 # reverse subtract / reverse subtract with carry r2 - r1
mul r0, r1, r2 # multiply
# shift e rotazione tramite add

and r0, r1, r2 # bitwise and
orr r0, r1, r2 # bitwise or
eor r0, r1, r2 # bitwise xor
bic r0, r1, r2 # bitwise clear - ogni 1 in r2, mette a 0 in r1

mov r0, r1 # move r0 = r1
mov r0, #21 # move r0 = 21
mvn r0, r1 # move not r0 = not r1

b label # branch (salto, anche condizionato)
bne label # branch not equal ecc...
bl label # branch link - salta alla procedura e aggiunge il PC al registro link r14

cmp r0, r1 # compare (r0 - r1) e setta i flag di stato senza risultato

ldr r0, [r1] # load from memory r0 = mem[r1]
str r0, [r1] # store in memory mem[r1] = r0
ldm r0, {r1, r2} # load multiple r1 = mem[r0], r2 = mem[r0+4]
stm r0, {r1, r2} # store multiple mem[r0] = r1, mem[r0+4] = r2

# ldm<mode> r [!], {list of registers}
# stm<mode> r [!], {list of registers}
# con ! r viene aggiornato
# <mode> = {ia,ib,da,db} (increment after, increment before, decrement after, decrement before)
```

```cpp
// per la divisione di interi
int divide(int A, int B){
  int Q = 0; int R = A;
  while(R >= B){
    Q++;
    R = R - B;
  }
  return Q;
}
```
