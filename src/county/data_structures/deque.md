# Deque (Double-ended queue)

## Definiție

O coadă cu două capete (deque - double-ended queue) este o structură de date liniară care permite inserarea și ștergerea elementelor atât la început, cât și la sfârșit în timp constant \\(O(1)\\).

## Operații și exemple

### Operații de bază

#### push_front

Adaugă elementul \\(x\\) la începutul deque-ului.

```cpp
deque<int> d;          // d = []
d.push_front(1);       // d = [1]
d.push_front(2);       // d = [2, 1]
d.push_front(3);       // d = [3, 2, 1]
```

#### push_back

Adaugă elementul \\(x\\) la sfârșitul deque-ului.

```cpp
deque<int> d;          // d = []
d.push_back(1);        // d = [1]
d.push_back(2);        // d = [1, 2]
d.push_back(3);        // d = [1, 2, 3]
```

#### pop_front

Elimină primul element din deque.

```cpp
deque<int> d;          // d = []
d.push_back(1);        // d = [1]
d.push_back(2);        // d = [1, 2]
d.push_back(3);        // d = [1, 2, 3]
d.pop_front();         // d = [2, 3]
d.pop_front();         // d = [3]
```

#### pop_back

Elimină ultimul element din deque.

```cpp
deque<int> d;          // d = []
d.push_back(1);        // d = [1]
d.push_back(2);        // d = [1, 2]
d.push_back(3);        // d = [1, 2, 3]
d.pop_back();          // d = [1, 2]
d.pop_back();          // d = [1]
```

#### front

Returnează primul element din deque.

```cpp
deque<int> d;          // d = []
d.push_back(1);        // d = [1]
d.push_back(2);        // d = [1, 2]
cout << d.front();     // afișează 1
d.push_front(3);       // d = [3, 1, 2]
cout << d.front();     // afișează 3
```

#### back

Returnează ultimul element din deque.

```cpp
deque<int> d;          // d = []
d.push_back(1);        // d = [1]
d.push_back(2);        // d = [1, 2]
cout << d.back();      // afișează 2
d.push_back(3);        // d = [1, 2, 3]
cout << d.back();      // afișează 3
```

#### empty

Verifică dacă deque-ul este gol.

```cpp
deque<int> d;          // d = []
cout << d.empty();     // afișează true (1)
d.push_back(1);        // d = [1]
cout << d.empty();     // afișează false (0)
d.pop_front();         // d = []
cout << d.empty();     // afișează true (1)
```

#### size

Returnează numărul de elemente din deque.

```cpp
deque<int> d;          // d = []
cout << d.size();      // afișează 0
d.push_back(1);        // d = [1]
cout << d.size();      // afișează 1
d.push_front(2);       // d = [2, 1]
cout << d.size();      // afișează 2
d.pop_back();          // d = [2]
cout << d.size();      // afișează 1
```

## Complexitate

### Complexitate temporală

- Inserare la început/sfârșit: \\(O(1)\\)
- Ștergere de la început/sfârșit: \\(O(1)\\)
- Acces la primul/ultimul element: \\(O(1)\\)
- Verificare dacă este gol: \\(O(1)\\)
- Obținere dimensiune: \\(O(1)\\)

### Complexitate spațială

- \\(O(n)\\), unde \\(n\\) este numărul de elemente din deque

## Aplicații

[Deque](https://www.infoarena.ro/problema/deque)

### Descrierea soluției

O soluție de complexitate \\(O(N)\\) folosește o coadă cu două capete (double ended queue, deque). În această structură, valorile pot fi inserate sau eliminate atât pe la începutul, cât și pe la sfârșitul deque-ului, toate aceste operații având loc în timp \\(O(1)\\) amortizat. Se observă că dacă există două elemente \\(A_i\\) și \\(A_j\\) astfel încât \\(A_i \leq A_j\\) și \\(i > j\\), atunci \\(A_i\\) va fi mereu preferat pentru minim față de \\(A_j\\), pentru secvențele ce încep după poziția \\(i\\) (inclusiv). Din acest motiv, la fiecare pas \\(i\\), elementul curent \\(A_i\\) elimină de la finalul deque-ului toate elementele mai mari sau egale cu el, apoi este inserat la finalul cozii. În acest fel, elementele din deque sunt menținute în ordine crescătoare, deci minimul se va afla la început. Se elimină apoi minimul de la începutul cozii dacă acesta nu mai aparține secvenței curente (poziția lui este mai mică sau egală cu \\(i-K\\)). În final, se adună minimul la soluție.

### Soluție

```cpp
#include <fstream>
#include <deque>
using namespace std;

ifstream fin("deque.in");
ofstream fout("deque.out");

const int NMAX = 5e6 + 1;

int a[NMAX];

deque<int> dq;

int n, k;

int main()
{
    fin >> n >> k;
    for (int i = 1; i <= n; ++i)
        fin >> a[i];

    // configuram primele k numere
    for (int i = 1; i <= k; ++i)
    {
        while (!dq.empty() && a[dq.back()] >= a[i])
            dq.pop_back();
        dq.push_back(i);
    }

    long long sum = a[dq.front()];

    for (int i = k + 1; i <= n; ++i)
    {
        // la fiecare pas, gasim minum pentru intervalul [i - k + 1, i]
        int left = i - k + 1;
        // ne asiguram ca minimele din deque sunt in ordine crescatoare
        // in momentul in care primul element din deque nu se mai incadreaza intervalilui nostru,
        // trebuie sa gasim urmatoarea pozitie valabila ca fiind minimul pe interval
        // asadar, orice element pe care il introducem trebuie sa stearga elementele mai mari care se afla inaintea lui
        while (!dq.empty() && a[dq.back()] >= a[i])
            dq.pop_back();
        // verificam daca primul element se afla in intervalul nostru, daca nu, il eliminam din deque
        if (!dq.empty() && dq.front() < left)
            dq.pop_front();
        // adaugam noul index
        dq.push_back(i);
        // actualizam suma
        sum += a[dq.front()];
    }

    fout << sum << '\n';

    return 0;
}
```

[Rover](https://kilonova.ro/problems/888)

### Soluție

```cpp
#include <fstream>
#include <deque>
#include <limits.h>
#include <string.h>

using namespace std;

ifstream fin("rover.in");
ofstream fout("rover.out");

const int NMAX = 502;

int dx[] = {-1, 1, 0, 0};
int dy[] = {0, 0, -1, 1};

deque<pair<int, int>> q;
int a[NMAX][NMAX], maxi, cnt, n, g, s, d;
bool viz[NMAX][NMAX];
int lee[NMAX][NMAX];
char caz;

bool ok(int x, int y)
{
    return (x && y && x <= n && y <= n && viz[x][y] == 0);
}

void Zone()
{
    q.push_back(make_pair(1, 1));
    while (q.size())
    {
        int x = q.front().first;
        int y = q.front().second;
        q.pop_front();
        viz[x][y] = 1;
        for (int i = 0; i < 4; ++i)
        {
            int nx = x + dx[i];
            int ny = y + dy[i];
            if (ok(nx, ny))
            {
                lee[nx][ny] = INT_MAX;
                for (int k = 0; k < 4; ++k)
                {
                    int x1 = nx + dx[k];
                    int y1 = ny + dy[k];
                    if (viz[x1][y1] == 1)
                        lee[nx][ny] = min(lee[nx][ny], lee[x1][y1]);
                }
                if (nx == n && ny == n)
                {
                    q.clear();
                    break;
                }
                else if (a[nx][ny] < g)
                {
                    lee[nx][ny]++;
                    q.push_back(make_pair(nx, ny));
                }
                else
                    q.push_front(make_pair(nx, ny));
            }
        }
    }
}

bool Lee()
{
    memset(viz, 0, sizeof viz);
    q.clear();
    q.push_back(make_pair(1, 1));
    while (q.size())
    {
        int x = q.front().first;
        int y = q.front().second;
        q.pop_front();
        viz[x][y] = 1;
        for (int i = 0; i < 4; ++i)
        {
            int nx = x + dx[i];
            int ny = y + dy[i];
            if (ok(nx, ny))
            {
                if (nx == n && ny == n)
                    return 1;
                if (a[nx][ny] >= g)
                    q.push_front(make_pair(nx, ny));
            }
        }
    }
    return 0;
}

void solve()
{
    fin >> caz >> n;
    if (caz == '1')
    {
        fin >> g;
        for (int i = 1; i <= n; ++i)
            for (int j = 1; j <= n; ++j)
                fin >> a[i][j];
        Zone();
        fout << lee[n][n] << "\n";
    }
    else
    {
        s = INT_MAX;
        for (int i = 1; i <= n; ++i)
            for (int j = 1; j <= n; ++j)
            {
                fin >> a[i][j];
                if (a[i][j] < s)
                    s = a[i][j];
                if (a[i][j] > d)
                    d = a[i][j];
            }
        while (s <= d)
        {
            g = (s + d) / 2;
            if (Lee())
            {
                s = g + 1;
                if (g > maxi)
                    maxi = g;
            }
            else
                d = g - 1;
            q.clear();
        }
        fout << maxi << "\n";
    }
}

int main()
{
    solve();
    return 0;
}
```
