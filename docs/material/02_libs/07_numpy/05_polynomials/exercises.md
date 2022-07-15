# E7.5 - Operazioni polinomiali in NumPy

## Esercizio E7.5.1

Scriviamo la funzione `somma_polinomi(pol_1, pol_2)` che permetta di sommare due polinomi di grandezza arbitraria.

### Soluzione S7.5.1

```py
def somma_polinomi(pol_1, pol_2):
    if len(pol_1) < len(pol_2):
        while len(pol_1) < len(pol_2):
            pol_1.insert(0, 0)
    elif len(pol_2) < len(pol_1):
        while len(pol_2) < len(pol_1):
            pol_2.insert(0, 0)
    return [(pol_1[i] + pol_2[i]) for i in range(len(pol_1))]

somma_polinomi([0, 1, 2], [2, 2, 1])
somma_polinomi([1, 2], [2, 2, 1])    
somma_polinomi([1, 2], [2, 2, 2, 1])
```

## Esercizio E7.5.2

Scriviamo la funzione `calcola_media(array, pesi)` che restituisce il valor medio di un array; usiamo una lista. Il parametro `pesi` è opzionale; nel caso sia lasciato il valore opzionale (lista vuota), la media sarà aritmetica; in caso contrario, verifichiamo la coerenza delle dimensioni dei vettori e restituiamo la media pesata.

### Soluzione S7.5.2

```py
def calcola_media(array, pesi=[]):
    if pesi == []:
        return sum(array) / len(array)
    else:
        if len(pesi) == len(array):
            return sum([(pesi[i] * array[i]) for i in range(len(array))]) / sum(pesi)
    raise ValueError('La lunghezza dei pesi non corrisponde a quella degli array.')

calcola_media([5, 4, 5])
calcola_media([5, 4, 5], [0, 1, 0])
calcola_media([5, 4, 5], [0, 1])
```

## Esercizio E7.5.3

Scriviamo la funzione `descrivi(array)` che permette di descrivere un array in termini non parametrici, individuando mediana, deviazione standard e range interquartile (ovvero tra il 25-percentile ed il 75-percentile).

### Soluzione S7.5.2

```py
def descrivi(array):
    return (
        np.median(array),
        np.std(array),
        np.percentile(array, 25) - np.percentile(array, 75)
    )

descrivi(np.array([3, 5, 3, 2, 1, 8]))
```
