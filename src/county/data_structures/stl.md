# Structuri de Date STL

## Set

### Definiție

Un `set` este o structură de date care stochează elemente unice în ordine crescătoare. Implementarea se bazează pe un arbore binar de căutare echilibrat (Red-Black Tree), ceea ce asigură operații eficiente de căutare, inserare și ștergere.

### Operații și exemple

#### insert

Inserează un element în set.

```cpp
set<int> s;           // s = {}
s.insert(3);          // s = {3}
s.insert(1);          // s = {1, 3}
s.insert(4);          // s = {1, 3, 4}
s.insert(1);          // s = {1, 3, 4} (1 există deja)
```

#### erase

Șterge un element din set.

```cpp
set<int> s;           // s = {}
s.insert(1);          // s = {1}
s.insert(2);          // s = {1, 2}
s.insert(3);          // s = {1, 2, 3}
s.erase(2);           // s = {1, 3}
```

#### find

Caută un element în set și returnează un iterator către acesta.

```cpp
set<int> s = {1, 2, 3, 4, 5};
auto it = s.find(3);  // it -> 3
if(it != s.end())     // elementul există
    cout << *it;      // afișează 3
it = s.find(6);       // it == s.end()
```

#### lower_bound

Returnează un iterator către primul element mai mare sau egal cu valoarea dată.

```cpp
set<int> s = {1, 3, 5, 7, 9};
auto it = s.lower_bound(4);  // it -> 5
it = s.lower_bound(5);       // it -> 5
it = s.lower_bound(6);       // it -> 7
```

#### upper_bound

Returnează un iterator către primul element strict mai mare decât valoarea dată.

```cpp
set<int> s = {1, 3, 5, 7, 9};
auto it = s.upper_bound(4);  // it -> 5
it = s.upper_bound(5);       // it -> 7
it = s.upper_bound(9);       // it == s.end()
```

### Complexitate

- Inserare: \\(O(\log n)\\)
- Ștergere: \\(O(\log n)\\)
- Căutare: \\(O(\log n)\\)
- lower_bound/upper_bound: \\(O(\log n)\\)

## Unordered Set

### Definiție

Un `unordered_set` este o structură de date care stochează elemente unice fără a le menține într-o ordine specifică. Implementarea se bazează pe o tabelă de dispersie (hash table).

### Operații și exemple

#### insert

```cpp
unordered_set<int> s;  // s = {}
s.insert(3);           // s = {3}
s.insert(1);           // s = {1, 3}
s.insert(4);           // s = {4, 1, 3}
```

#### find

```cpp
unordered_set<int> s = {1, 2, 3, 4, 5};
auto it = s.find(3);   // it -> 3
if(it != s.end())      // elementul există
    cout << *it;       // afișează 3
```

### Complexitate

- Inserare: \\(O(1)\\) amortizat
- Ștergere: \\(O(1)\\) amortizat
- Căutare: \\(O(1)\\) amortizat

## Multiset

### Definiție

Un `multiset` este similar cu `set`, dar permite elemente duplicate. Menține elementele sortate.

### Operații și exemple

#### insert

```cpp
multiset<int> ms;     // ms = {}
ms.insert(3);         // ms = {3}
ms.insert(3);         // ms = {3, 3}
ms.insert(1);         // ms = {1, 3, 3}
```

#### count

```cpp
multiset<int> ms = {1, 2, 2, 2, 3};
cout << ms.count(2);  // afișează 3
```

### Complexitate

- Inserare: \\(O(\log n)\\)
- Ștergere: \\(O(\log n)\\)
- Căutare: \\(O(\log n)\\)

## Map

### Definiție

Un `map` este o structură de date care stochează perechi cheie-valoare unice, ordonate după cheie.

### Operații și exemple

#### insert/operator[]

```cpp
map<string, int> m;           // m = {}
m["ana"] = 1;                // m = {("ana", 1)}
m.insert({"bob", 2});        // m = {("ana", 1), ("bob", 2)}
m["ana"] = 3;                // m = {("ana", 3), ("bob", 2)}
```

#### find

```cpp
map<string, int> m = {{"ana", 1}, {"bob", 2}};
auto it = m.find("ana");     // it -> ("ana", 1)
if(it != m.end())
    cout << it->second;      // afișează 1
```

### Complexitate

- Inserare: \\(O(\log n)\\)
- Ștergere: \\(O(\log n)\\)
- Căutare: \\(O(\log n)\\)

## Unordered Map

### Definiție

Un `unordered_map` este similar cu `map`, dar folosește o tabelă de dispersie și nu menține ordinea elementelor.

### Operații și exemple

#### insert/operator[]

```cpp
unordered_map<string, int> m;  // m = {}
m["ana"] = 1;                  // m = {("ana", 1)}
m.insert({"bob", 2});          // m = {("bob", 2), ("ana", 1)}
```

### Complexitate

- Inserare: \\(O(1)\\) amortizat
- Ștergere: \\(O(1)\\) amortizat
- Căutare: \\(O(1)\\) amortizat

## Multimap

### Definiție

Un `multimap` este similar cu `map`, dar permite chei duplicate. Elementele sunt ordonate după cheie.

### Operații și exemple

#### insert

```cpp
multimap<string, int> mm;      // mm = {}
mm.insert({"ana", 1});         // mm = {("ana", 1)}
mm.insert({"ana", 2});         // mm = {("ana", 1), ("ana", 2)}
```

#### equal_range

```cpp
multimap<string, int> mm = {{"ana", 1}, {"ana", 2}, {"bob", 3}};
auto range = mm.equal_range("ana");
for(auto it = range.first; it != range.second; ++it)
    cout << it->second << " ";  // afișează 1 2
```

### Complexitate

- Inserare: \\(O(\log n)\\)
- Ștergere: \\(O(\log n)\\)
- Căutare: \\(O(\log n)\\)

## Observații generale

1. Structurile ordonate (`set`, `map`, `multiset`, `multimap`):

   - Mențin elementele sortate
   - Folosesc arbori binari de căutare echilibrați
   - Au complexitate logaritmică pentru operațiile de bază
   - Suportă operații de tip `lower_bound`/`upper_bound`

2. Structurile neordonate (`unordered_set`, `unordered_map`):

   - Nu mențin o ordine specifică
   - Folosesc tabele de dispersie
   - Au complexitate constantă amortizată pentru operațiile de bază
   - Nu suportă operații de tip `lower_bound`/`upper_bound`
   - Pot avea performanță mai slabă în cazul multor coliziuni

3. Structurile multi (`multiset`, `multimap`):
   - Permit elemente/chei duplicate
   - Oferă operații suplimentare pentru gestionarea duplicatelor (count, equal_range)
   - Mențin ordinea elementelor

## Aplicații

### [Turnuri](https://kilonova.ro/problems/902)

#### Descrierea soluției

Cheia problemei este să determinăm cele mai apropiate două turnuri mai înalte decât fiecare turn în parte, atât în stânga, cât și în dreapta. Menținem perechi de forma \\((h_i, i)\\) într-un vector. Având în vedere că toate înălțimile sunt diferite, putem să folosim un set și să le prelucrăm în ordine descrescătoare a înălțimilor. Așadar, sortăm vectorul și îl parcurgem în ordine descrescătoare. Folosim un set în care vom reține indicii turnurilor pe care le-am vizitat. Pentru fiecare turn în parte, vom căuta, folosind `upper_bound`, poziția unde se află în dreapta primul turn mai înalt decât turnul curent. Următorul turn după acesta, adică al doilea turn mai înalt decât turnul curent, va fi chiar următorul element din set. Pentru a le determina pe cele două turnuri din stânga, trebuie să mergem înapoi, folosindu-ne de iteratorul returnat de `upper_bound` pentru turnul curent. La final, vom adăuga în set turnul curent.

Pentru a determina totalul, vom menține un vector ce indică cu cât se modifică gradul de frumusețe în momentul în care turnul curent dispare. Așadar, pentru fiecare turn în parte, determinăm în \\(O(1)\\) noul grad de frumusețe al orașului.

#### Soluție

```cpp
#include <fstream>
#include <vector>
#include <algorithm>
#include <set>

using namespace std;

ifstream fin("turnuri.in");
ofstream fout("turnuri.out");

typedef pair<int, int> p;

set<int> s;
vector<p> turnuri;
vector<p> l;
vector<p> r;
vector<long long> offset;

int n, m;

int main()
{
    fin >> n;
    l.resize(n + 1);
    r.resize(n + 1);
    offset.resize(n + 2, 0);
    for (int i = 1; i <= n; ++i)
    {
        l[i] = {-1, -1};
        r[i] = {-1, -1};

        fin >> m;
        turnuri.push_back({m, i});
    }

    sort(turnuri.begin(), turnuri.end(), greater<p>());

    for (int i = 0; i < n; ++i)
    {
        if (!s.empty())
        {
            auto closest = s.upper_bound(turnuri[i].second);

            if (closest != s.end())
            {
                r[turnuri[i].second].first = *closest;
                auto cpy = closest;
                ++cpy;
                if (cpy != s.end())
                {
                    r[turnuri[i].second].second = *cpy;
                }
            }

            if (closest != s.begin())
            {
                --closest;
                l[turnuri[i].second].first = *closest;
                if (closest != s.begin())
                {
                    --closest;
                    l[turnuri[i].second].second = *closest;
                }
            }
        }
        s.insert(turnuri[i].second);
    }

    long long total = 0;
    for (int i = 1; i <= n; ++i)
    {
        int left_limit = l[i].first != -1 ? l[i].first : 0;
        int left_limit2nd = l[i].second != -1 ? l[i].second : 0;
        int right_limit = r[i].first != -1 ? r[i].first : n + 1;
        int right_limit2nd = r[i].second != -1 ? r[i].second : n + 1;

        offset[left_limit] += left_limit - left_limit2nd;
        offset[right_limit] += right_limit2nd - right_limit;

        total += right_limit - left_limit - 1;
    }
    for (int i = 1; i <= n; ++i)
    {
        int left_limit = l[i].first != -1 ? l[i].first : 0;
        int right_limit = r[i].first != -1 ? r[i].first : n + 1;
        fout << total - (right_limit - left_limit - 1) + offset[i] + 1 << '\n';
    }
    return 0;
}
```

### [Mod](https://kilonova.ro/problems/3606)

#### Descrierea soluției

Menținem o structură de date care să ne permită să știm care este valoarea maximă a unui element și care este poziția acestuia. În set vom menține perechi de forma \\((v_i, i)\\), sortate descrescător după valoare. Pentru query-uri de tip 1, cât timp avem operații de făcut și primul element din set va fi mai mare decât `k`, îl vom șterge și îl vom înlocui cu `v_i \% k`. Pentru query-uri de tip 2, vom actualiza elementul de pe poziția `x` și îl vom adăuga pe cel de valoare `k`. Pentru query-uri de tip 3, vom afișa valoarea maximă din set.

#### Soluție

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <set>

using namespace std;

ifstream fin("mod.in");
ofstream fout("mod.out");

set<pair<int, int>, greater<pair<int, int>>> s;

int n, q;

int main()
{
    fin >> n >> q;
    vector<int> v(n + 1);

    for (int i = 1; i <= n; ++i)
    {
        fin >> v[i];
        s.insert({v[i], i});
    }

    int c, x, k;

    while (q--)
    {
        fin >> c;
        if (c == 3)
            fout << (*s.begin()).first << '\n';
        else
        {
            fin >> x >> k;
            if (c == 2)
            {
                s.erase({v[x], x});
                v[x] = k;
                s.insert({v[x], x});
            }
            else
            {
                while (x && !s.empty() && ((*s.begin()).first >= k))
                {
                    auto p = *s.begin();
                    s.erase(p);
                    v[p.second] = p.first % k;
                    s.insert({v[p.second], p.second});
                    --x;
                }
            }
        }
    }

    return 0;
}
```

### [Muguraș](https://kilonova.ro/problems/2573)

#### [Descrierea soluției](http://moisil.edubh.ro/wp-content/uploads/2024/04/10_muguras-descriere-1.pdf)

#### Soluție

```cpp
#include <iostream>
#include <fstream>
#include <sstream>
#include <unordered_map>

using namespace std;

ifstream fin("muguras.in");
ofstream fout("muguras.out");

unordered_map<string, pair<string, unsigned long long>> m;

int n;
string s, v, a;

int main()
{
    fin >> n;

    fin >> s >> v;
    fin.get();
    while (n--)
    {
        getline(fin, a);
        istringstream iss(a);
        string op1, sign, op2, op3;

        iss >> op1 >> sign;

        if (sign[0] == ':')
        {
            iss >> op2;
            unsigned long long cnt = 0;
            for (int i = 0; i <= (int)op2.size() - (int)s.size(); ++i)
            {
                int index = 0;
                bool ok = true;
                for (int j = i; j < i + s.size(); ++j)
                {
                    if (op2[j] != s[index])
                    {
                        ok = false;
                        break;
                    }
                    else
                        ++index;
                }
                cnt += ok;
            }
            m[op1] = make_pair(op2, cnt);
            // cout << op1 << " " << m[op1].first << " " << m[op1].second << endl;
        }
        else
        {
            iss >> op2 >> sign >> op3;
            unsigned long long cnt = m[op2].second + m[op3].second;
            op2 = m[op2].first;
            op3 = m[op3].first;
            // cout << op2 << " " << op3 << " " << cnt << endl;
            for (int lenop2 = 1; lenop2 < s.size(); ++lenop2)
            {
                if (lenop2 > op2.size())
                {
                    break;
                }
                int lenop3 = s.size() - lenop2;
                if (lenop3 > op3.size())
                {
                    continue;
                }
                int index = 0;
                bool ok = true;
                for (int i = op2.size() - lenop2; i < op2.size(); ++i)
                {
                    if (op2[i] != s[index])
                    {
                        ok = false;
                        break;
                    }
                    else
                        ++index;
                }
                if (ok)
                {
                    for (int i = 0; i < lenop3; ++i)
                    {
                        if (op3[i] != s[index])
                        {
                            ok = false;
                            break;
                        }
                        else
                            ++index;
                    }
                }
                cnt += ok;
            }

            string con, f = op2 + op3;

            for (int i = 0; i < min(s.size(), f.size()); ++i)
            {
                con += f[i];
            }

            for (int i = max(s.size(), f.size() - s.size()); i < f.size(); ++i)
                con += f[i];

            m[op1] = make_pair(con, cnt);
            // cout << op1 << " din 2 " << m[op1].first << " " << m[op1].second << endl;
        }
    }

    fout << m[v].second << endl;

    return 0;
}
```
