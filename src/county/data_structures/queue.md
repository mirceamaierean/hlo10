### Coada (Queue) – Structură de Date

O coadă (queue) este o structură de date abstractă în care:

- Adăugarea unui element se face la un capăt (coada).
- Eliminarea unui element se face la celălalt capăt (începutul cozii).

În orice moment avem acces doar la elementul din față, adică cel care urmează să fie eliminat.

---

## Operații cu coada

O coadă permite următoarele operații fundamentale:

- Inițializarea cozii – crearea unei cozi vide.
- Verificarea dacă o coadă este vidă.
- Adăugarea unui nou element (push).
- Eliminarea unui element (pop).
- Accesarea primului element din coadă (front).

---

## Exemplu din viața reală

Funcționarea unei cozi este similară unei cozi la casa de bilete:

- Spectatorii sosesc și se așază la coadă în ordinea în care au venit.
- Ordinea în care cumpără biletele este exact aceeași.

Acest mecanism se numește FIFO _(First In, First Out)_ – Primul intrat, primul ieșit.

---

## Când folosim coada

Utilizăm coada când trebuie să procesăm informații într-o ordine precisă, pe măsură ce acestea sunt identificate.

### Procesul de expandare a cozii:

1. Adăugăm în coadă informații inițiale.
2. Cât timp coada nu este vidă _(sau până obținem rezultatul dorit)_:
   - Extragem un element.
   - Folosindu-l, identificăm informații noi și le adăugăm în coadă.

---

## Utilizări ale cozii în informatică

Exemple practice de utilizare a cozii:

- Tipărirea documentelor la imprimantă – Documentele sunt adăugate într-o coadă de așteptare, iar imprimarea se face în ordinea sosirii.
- Evaluarea soluțiilor pe pbinfo.ro – Problemele sunt procesate în ordinea postării, folosind o coadă.

---

## Modalități de implementare a cozii

Coada poate fi implementată în C++ în mai multe moduri:

1. Implementare statică – folosind tablouri.
2. Implementare dinamică – folosind liste alocate dinamic.
3. Folosirea containerului `queue` din STL _(Standard Template Library)_.

În acest articol vom explora:

- Implementarea statică.
- Folosirea STL `queue`.

---

## Implementarea statică a cozii

Vom folosi:

- Un tablou unidimensional `Q[]` pentru a stoca elementele.
- Două variabile: `st` și `dr`, care marchează începutul și sfârșitul cozii.

Observație:

- `st` provine de la stânga (start).
- `dr` provine de la dreapta (end).
- Adăugarea se face în `Q[dr]`, iar eliminarea prin creșterea lui `st`.

---

### Declarații

```cpp
const int DIM = 1000;
int Q[DIM], st, dr;
```

### Inițializarea cozii (creare coadă vidă)

```cpp
st = 1;
dr = 0;
```

### Verificarea dacă coada este vidă

```cpp
if (st > dr) // Coada este VIDĂ
if (st <= dr) // Coada NU este vidă
```

### Adăugarea unui element (`PUSH`)

```cpp
Q[++dr] = _VALOARE;
```

### Eliminarea unui element (`POP`)

```cpp
st++;
```

### Accesarea primului element (`FRONT`)

```cpp
Q[st];
```

---

## Folosirea containerului `queue` din STL

STL oferă containerul `queue`, care simplifică gestionarea cozilor.

### Declarații

```cpp
#include <queue>
using namespace std;
```

### Inițializarea cozii

```cpp
queue<int> Q;
```

### Verificarea dacă coada este vidă

```cpp
Q.empty(); // Returnează true dacă este vidă, false altfel.
```

### Adăugarea unui element (`PUSH`)

```cpp
Q.push(_VALOARE);
```

### Eliminarea unui element (`POP`)

```cpp
Q.pop();
```

### Accesarea primului element (`FRONT`)

```cpp
Q.front();
```

---

## Aplicații

### Algoritmul lui Lee

[Alee](https://kilonova.ro/problems/768)

#### Soluție

```cpp
#include <fstream>
#include <queue>

using namespace std;

ifstream fin("alee.in");
ofstream fout("alee.out");

const int NMAX = 180;

int n, m, a[NMAX][NMAX];
int xs, ys, xf, yf, x, y;

// definim vectorii de directie
int dx[] = {-1, 1, 0, 0};
int dy[] = {0, 0, -1, 1};

// initializam o coada
bool ok(int &x, int &y)
{
    // 1) valoarea lui a[x][y] sa fie 0
    // 2) sa nu fi fost vizitat inainte (cost = 0)
    // 3) x > 0 si x <= n
    // 4) y > 0 si y <= n
    return a[x][y] == 0 && x > 0 && x <= n && y > 0 && y <= n;
}

void lee(queue<pair<int, int>> &q)
{
    // inseram cel mult o data fiecare pozitie => O(n ^ 2)
    while (!q.empty())
    {
        x = q.front().first;
        y = q.front().second;
        q.pop();

        if (x == xf && y == yf)
            return;

        for (int i = 0; i < 4; ++i)
        {
            int nx = x + dx[i];
            int ny = y + dy[i];
            if (ok(nx, ny))
            {
                a[nx][ny] = a[x][y] + 1;
                q.push({nx, ny});
            }
        }
    }
}

int main()
{
    fin >> n >> m;
    for (int i = 1; i <= m; ++i) // O(m) citire
    {
        fin >> x >> y;
        a[x][y] = -1;
    }

    fin >> xs >> ys >> xf >> yf;

    a[xs][ys] = 1;

    queue<pair<int, int>> q; // retinem x si y

    q.push({xs, ys});
    lee(q);

    fout << a[xf][yf] << '\n';

    return 0;
}
```
