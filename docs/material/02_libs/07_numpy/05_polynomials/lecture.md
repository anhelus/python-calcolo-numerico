# 7.5 - Operazioni polinomiali in NumPy

Il modulo `numpy.polynomial.polynomial` ci offre numerose classi e funzionalità per il trattamento dei polinomi. Vediamo quali sono le principali.

Immaginiamo di avere due diversi polinomi (cui non assoceremo alcun significato fisico), ovvero:

$$
\begin{cases}
c1: 2x + 1 \\
c2: x^2 + 3x + 2
\end{cases}
$$

Vediamo come usare dei metodi forniti dal modulo `polynomial` per effettuare delle operazioni su di loro.

Prima di partire, però, introduciamo gli oggetti di classe `poly1d`, che ci permettono di rappresentare in maniera compiuta un polinomio. In particolare, partendo dai coefficienti di un generico polinomio `p`, potremo ottenere un oggetto `poly1d` invocando l'omonimo costruttore:

```py
p_pol = np.poly1d(p)
```

Il vantaggio principale degli oggetti `poly1d` sta sia nella loro rappresentazione, sia nel fatto che possono essere direttamente utilizzati all'interno delle funzioni per il calcolo polinomiale che vedremo nel seguito.

## 7.5.1 - Addizione di polinomi

Per effettuare l'addizione di due polinomi, possiamo usare il metodo `polyadd(c1, c2)`, che accetta come parametri due vettori `c1` e `c2` che rappresentano, rispettivamente, i coefficienti del polinomio 1 e 2. Volendo sommare il primo ed il secondo polinomio, potremo scrivere:

```py
>>> from numpy.polynomial import polynomial as poly
>>> c1 = (0, 2, 1)
>>> c2 = (1, 3, 2)
>>> poly.polyadd(c1, c2)
```

Questa operazione ci darà il risultato atteso, ovvero $x^2 + 5x + 3$.

Notiamo come le dimensioni di `c1` e di `c2` debbano essere tra loro *coerenti*. Se infatti omettessimo il coefficiente $0$ al termine di secondo grado in `c1`, il risultato sarebbe il seguente:

```py
>>> c3 = (2, 1)
>>> poly.polyadd(c3, c2)
array([3., 4., 2.])
```

Ovviamente, il risultato precedente può essere errato in base al valore assunto dal polinomio `c3`.

## 7.5.2 - Sottrazione di polinomi

Possiamo poi sottrarre due polinomi usando la funzione `polysub(c1, c2)`, i cui parametri sono identici a quelli passati a `polyadd()`:

```py
>>> poly.polysub(c2, c1)
array([1., 1., 1.])
```

## 7.5.3 - Moltiplicazione di polinomi

Le considerazioni precedenti possono essere banalmente traslate al caso della moltiplicazione tra polinomi, ottenibile mediante la funzione `polymul(c1, c2)`.

```py
>>> poly.polymul(c1, c2)
array([0., 2., 7., 7., 2.])
```

!!!warning "Attenzione!"
    Nelle ultime versioni di NumPy, i coefficienti sono ordinati da quello a grado più basso a quello di grado più alto!

## 7.5.4 - Divisione tra polinomi

La divisione tra polinomi è un'operazione leggermente più complessa delle altre, e prevede l'uso della funzione `polydiv(c1, c2)`, che restituirà stavolta due array: il primo, `q`, rappresenta i coefficienti del polinomio quoziente, mentre il secondo, `r`, indica i coefficienti del polinomio resto.

Nel nostro caso:

```py
>>> (q, r) = poly.polydiv(c1, c2)
>>> q; r
array([0.5])
array([-0.5,  0.5])
```

Anche in questo caso, i coefficienti sono ordinati da quello a grado più basso a quello a grado più alto.

## 7.5.5 - Elevazione a potenza

Chiudiamo questa breve panoramica parlando dell'elevazione a potenza di un polinomio, effettuabile mediante la funzione `polypow(c, pow)`, con `c` vettore dei coefficienti, e `pow` potenza a cui elevare:

```py
>>> poly.polypow(c1, 2)
array([0., 0., 4., 4., 1.])
```

Anche in questo caso, vengono riportati i termini pari a zero nei risultati.

## 7.5.6 - Valore assunto da un polinomio

Per valutare il valore $y$ assunto dal polinomio per un determinato valore di $x$, usiamo la funzione `polyval(x, p)`, che accetta come argomento un intero (o una lista di interi) `x` ed un polinomio `p`.

Se volessimo valutare il valore assunto da $y$ per $x \in [1, 2]$ sulla retta rappresentata dal polinomio `c1`, ad esempio, potremmo usare `polyval()` come segue:

```py
>>> poly.polyval([1, 2], c1)
array([3., 8.])
```

## 7.5.7 - Derivata ed integrale di funzioni polinomiali

Concludiamo questa breve carrellata con due metodi in grado di calcolare, rispettivamente, la derivata e l'integrale di una funzione polinomiale.

Il metodo `polyder(p, m)`, infatti, permette di calcolare la derivata di ordine `m` del polinomio `p` (di default, `m=2`):

```py
>>> poly.polyder(c1)
array([2., 2.])
```

Il metodo duale è `polyint(p, m)`, che prevedibilmente calcola l'integrale di ordine `m` del polinomio `p`:

```py
>>> poly.polyint(c1)
array([0., 0., 1., 0.33333333])
```

!!!warning "Attenzione"
    Entrambe le funzioni si aspettano i coefficienti del polinomio passato ordinati dal grado più basso a quello più alto.
