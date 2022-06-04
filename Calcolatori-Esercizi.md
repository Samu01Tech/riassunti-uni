<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>

# Calcolatori (Esercizi)

## Ottimizzazione pipeline

> Vengono dati i tempi di esecuzione delle varie parti del processore. Calcolare l'ottimizzazione massima utilizzando il sistema pipeline.

$fetch = 600_{ps}$

$decodifica = 600_{ps}$

$ALU = 500_{ps}$

$memoria = 400_{ps}$

$scritturaReg = 700_{ps}$

$$\frac{600+600+500+400+700}{700} = 4\ volte\ più\  veloce$$

## Cache mapping

> Vengono dati dimensione della cache, dimensione dei blocchi e un indirizzo. Calcolare il blocco a cui punta l'indirizzo.

$Cache_{dim} = 4KB$

$Block_{dim} = 16 byte$

$Address = 0x1F164$

1. Calcolo il numero di blocchi
   $\frac{4096}{16} = 256 _{blocchi}$
2. Converto l'indirizzo in decimale
   $0x1F164 \rArr 127332$
3. Calcolo l'indirizzo del blocco
   $\frac{127332}{16} = 7958,25 = 7958$
4. Calcolo il numero del blocco
   $7958mod256 = 22$

## Cache miss

> Calcolare il CPI effettivo

- CPI_ideale = 3,
- miss_cache_istruzioni = 1.5%,
- miss_cache_dati = 5%,
- time_cache_miss = 150,
- istruzioni_memoria = 30%.

$$3+(0.015 \cdot 150)+(0.05 \cdot 30 \cdot 150) = 7.5$$
