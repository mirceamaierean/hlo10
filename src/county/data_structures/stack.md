# Stack

**Stiva** (stack) este o structură de date liniară abstractă, pentru care sunt definite operațiile de adăugare a unui element și eliminare a unui element și aceste operații se realizează la un singur capăt al structurii, numit **vârful stivei**.

În timpul operațiilor cu stiva avem acces numai la elementul din vârful stivei.

## Operații cu stiva

Cu o stivă se pot face următoarele operații:

- inițializarea stivei – crearea unei stive vide;
- verificarea faptului că o stivă este sau nu vidă;
- adăugarea unui nou element pe stivă – elementul devine _vârful stivei_. Operația se numește **push**;
- eliminarea unui element de pe stivă – se va elimina _vârful stivei_. Un nou element devine vârf al stivei, sau ea devine vidă. Operația se numește **pop**;
- identificarea valorii elementului din vârful stivei – accesul la acel element Operația se numește **top**.

Imaginați-vă o stivă de lăzi într-un depozit. Dacă adăugăm încă o ladă, o vom plasa în vârful stivei. Dacă luăm o ladă, o vom lua pe cea din vârful stivei – altfel s-ar răsturna stiva!!

Deoarece operațiile cu elementele stivei se fac la același capăt, spunem că stiva este o structură de date de tip **LIFO** – Last In First Out (ultimul intrat, primul ieșit).

## Când folosim stiva?

Programele au la dispoziție memorie, iar o parte a ei se numește _de tip stivă_ – STACK, tocmai pentru că operațiile cu această memorie se fac pe principiul stivei. Apelul functiilor, deci și recursivitatea, folosesc memoria de tip stivă, iar înțelegerea acestui concept cere înțelegerea modului în care funcționează o stivă.

În programe putem folosi stiva atunci când vrem să amânăm efectuarea unor operații până la obținerea unor rezultate. De exemplu, conversia unui număr din baza 10 în baza 2 constă în efectuarea succesivă a unor împărțiri la `2`. Cifrele reprezentării în baza `2` sunt resturile împărțirii în ordine inversă. Ne putem imagina că la fiecare împărțire plasăm restul pe o stivă. În final golim stiva și afișăm valorile întâlnite.

## Modalități de implementare a stivei

Stiva poate fi implementată în limbajul C++ în mai multe moduri:

- implementare statică, prin intermediul tablourilor;
- implementare dinamică, prin intermediul listelor alocate dinamic;
- folosirea containerului `stack` din STL.

### Implementarea statică a stivei

Vom folosi un tablou alocat static și o variabilă simplă prin care identificăm vârful stivei. În continuare considerăm o stivă cu elemente întregi.

**Declarații**

```
const int DIM = 100;
int S[DIM], vf;
```

**Inițializarea stivei** – crearea unei stive vide

```
vf = 0;
```

**Verificarea faptului că stiva este vidă**

```
vf == 0 // stivă vidă
vf > 0 // stivă nevidă
```

**Adăugarea unui element – PUSH**

```
S[vf++] = \_VALOARE ;
```

**Eliminarea unui element – POP**

```
vf--;
```

**Identificarea valorii din vârful stivei – TOP**

```
S[vf-1]
```

### Folosirea containerului STL stack

Standard Template Library pune la dispoziție un container adaptor specializat pentru gestionarea unei stive, numit `stack`. Un obiect de tip `stack` încapsulează toate operațiile specifice stivei:

**Declarații**

```cpp
#include <stack>
```

**Inițializarea stivei** – crearea unei stive vide

```cpp
stack<T> S; // T este tipul elementelor stivei, poate sa fie orice tip de date (int, float, double, etc.)
```

**Verificarea faptului că stiva este vidă**

```cpp
S.empty() // true dacă stiva este vidă, false în caz contrar
```

**Adăugarea unui element – PUSH**

```cpp
S.push( \_VALOARE );
```

**Eliminarea unui element – POP**

```cpp
S.pop();
```

**Identificarea valorii din vârful stivei – TOP**

```cpp
S.top()
```

---

## Aplicații: Determinarea celui mai apropiat număr mai mic

[Skyline](https://www.pbinfo.ro/probleme/2728/skyline)

### Descrierea soluției

Vom folosi o stivă pentru a determina pentru fiecare element cel mai apropiat număr mai mic. Vom parcurge vectorul și pentru fiecare element vom verifica dacă este mai mic decât elementul din vârful stivei. Dacă da, vom elimina elementul din vârful stivei și vom adăuga elementul curent în stivă. Dacă nu, vom adăuga elementul curent în stivă. În stivă, toate elementele vor fi în ordine crescătoare, așadar, când vârful acesteia este mai mare decât elementul curent, înseamnă că am găsit cel mai apropiat număr mai mic din dreapta vârfului stivei. Analog, dacă descoperim în vârful stivei un element mai mic decât elementul curent, înseamnă că am găsit cel mai apropiat număr mai mic din stânga elementului curent. De asemenea, vom calcula suma elementelor din stivă pentru fiecare element.

### Soluție

```cpp
#include <fstream>
#include <stack>

using namespace std;

const int NMAX = 40005;

struct skyline
{
    int val, s, d, suma;
};

skyline a[NMAX];

ifstream fin("skyline.in");
ofstream fout("skyline.out");

int n;

stack <int> st;

int main()
{
    fin >> n;

    for (int i = 1; i <= n; ++i)
    {
        fin >> a[i].val >> a[i].suma;
        a[i].suma += a[i - 1].suma;

        a[i].s = 0;
        a[i].d = n;
        while (!st.empty() && a[st.top()].val >= a[i].val)
        {
            a[st.top()].d = i - 1;
            st.pop();
        }

        if (!st.empty()) a[i].s = st.top();

        st.push(i);
    }

    int64_t maxi = 0;

    for (int i = 1; i <= n; ++i)
    {
        unsigned long long val = 1LL * (a[a[i].d].suma - a[a[i].s].suma) * a[i].val;
        maxi = (val > maxi) ? val : maxi;
    }
    fout << maxi << "\n";

    return 0;
}
```

## Aplicații: Evaluarea expresiilor aritmetice

[Evaluare](https://www.infoarena.ro/problema/evaluare)

### Descrierea soluției

O expresie matematică conținând numere și operatori este dată sub formă de șir de caractere.  
Scopul este să evaluăm valoarea acesteia în \\( O(n) \\), unde \\( n \\) este lungimea expresiei.

Algoritmul discutat aici transformă expresia într-o notație poloneză inversată (implicit sau explicit) și evaluează rezultatul.

#### Notația poloneză inversată (Reverse Polish Notation - RPN)

Notația poloneză inversată (RPN) este o metodă de scriere a expresiilor matematice, în care operatorii sunt plasați după operanzi. De exemplu, expresia:

$$
a + b \cdot c \cdot d + (e - f) \cdot (g \cdot h + i)
$$

poate fi rescrisă în notație poloneză inversată astfel:

$$
a  b c \cdot d \cdot + \quad ef - g h \cdot i + \cdot  +
$$

Expresiile în această formă sunt ușor de evaluat în timp \\(O(n)\\), utilizând o stivă:

1. Parcurgem elementele expresiei.
2. Dacă întâlnim un **operand**, îl punem în stivă.
3. Dacă întâlnim un **operator**, extragem **ultimii doi operanzi**, aplicăm operația și punem rezultatul înapoi în stivă.
4. La final, în stivă rămâne exact **valoarea expresiei**.

Pentru început, considerăm expresii simplificate:

- Toți operatorii sunt binari (au doi operanzi).
- Toți operatorii sunt asociativi la stânga (se execută de la stânga la dreapta).
- Expresiile pot conține paranteze.

Folosim două stive:

1. Stiva pentru numere – stochează operanzii.
2. Stiva pentru operatori și paranteze – respectă o ordine strict descrescătoare a priorităților operatorilor.

Parcurgem expresia caracter cu caracter:

1. Dacă e un număr, îl punem în stiva numerelor.
2. Dacă e o paranteză deschisă `(`, o punem în stiva operatorilor.
3. Dacă e o paranteză închisă `)`, efectuăm toate operațiile din stivă până la `(`.
4. Dacă e un operator, eliminăm operatorii din stivă până când găsim unul cu prioritate mai mică și punem operatorul curent în stivă.
5. După parcurgerea expresiei, executăm operatorii rămași în stivă.

### Soluție

```cpp
#include <iostream>
#include <fstream>
#include <stack>

using namespace std;

ifstream fin("evaluare.in");
ofstream fout("evaluare.out");

bool is_op(char c)
{
    return c == '+' || c == '-' || c == '*' || c == '/';
}

int priority(char op)
{
    if (op == '+' || op == '-')
        return 1;
    if (op == '*' || op == '/')
        return 2;
    return -1;
}

void process_op(stack<int> &st, char op)
{
    int r = st.top();
    st.pop();
    int l = st.top();
    st.pop();
    switch (op)
    {
    case '+':
        st.push(l + r);
        break;
    case '-':
        st.push(l - r);
        break;
    case '*':
        st.push(l * r);
        break;
    case '/':
        st.push(l / r);
        break;
    }
}

int evaluate(string &s)
{
    stack<int> st;
    stack<char> op;
    for (int i = 0; i < (int)s.size(); i++)
    {
        if (s[i] == '(')
        {
            op.push('(');
        }
        else if (s[i] == ')')
        {
            while (op.top() != '(')
            {
                process_op(st, op.top());
                op.pop();
            }
            op.pop();
        }
        else if (is_op(s[i]))
        {
            char cur_op = s[i];
            while (!op.empty() && priority(op.top()) >= priority(cur_op))
            {
                process_op(st, op.top());
                op.pop();
            }
            op.push(cur_op);
        }
        else
        {
            int number = 0;
            while (i < (int)s.size() && isalnum(s[i]))
                number = number * 10 + s[i++] - '0';
            --i;
            st.push(number);
        }
    }

    while (!op.empty())
    {
        process_op(st, op.top());
        op.pop();
    }
    return st.top();
}

int main()
{
    string s;
    fin >> s;
    fout << evaluate(s) << "\n";
    return 0;
}
```

### [Formație](https://kilonova.ro/problems/2571)

#### [Descrierea soluției](http://moisil.edubh.ro/wp-content/uploads/2024/04/10_formatie_descriere.pdf)

#### Soluție

```cpp
#include <iostream>
#include <fstream>
#include <stack>
#include <string.h>
#include <stdlib.h>
#include <string.h>
#include <assert.h>

using namespace std;

typedef struct
{
    int sus, jos, stanga, dreapta;
} limite;

const int NMAX = 501;
const long long MOD = 1e9 + 7;
int a[NMAX][NMAX], n, c;
limite l[NMAX][NMAX];

int spl[NMAX][NMAX], spc[NMAX][NMAX],   // sume partiale linii, sume partiale coloane
    sspl[NMAX][NMAX], sspc[NMAX][NMAX]; // sume de sume partiale pe linii, sume de sume partiale coloane

long long transform(long long x)
{
    if (x < 0)
        return (MOD * MOD + x) % MOD;
    return x % MOD;
}

ifstream fin("formatie.in");
ofstream fout("formatie.out");

void read()
{
    fin >> c >> n;
    for (int i = 1; i <= n; ++i)
        for (int j = 1; j <= n; ++j)
            fin >> a[i][j];
}

void computeLimits()
{
    stack<pair<int, int>> s;
    for (int i = 1; i <= n; ++i)
    {
        s = stack<pair<int, int>>();
        for (int j = 1; j <= n; ++j)
        {
            l[i][j].stanga = 1;
            l[i][j].dreapta = n;
            while (!s.empty() && a[i][j] < a[s.top().first][s.top().second])
            {
                l[i][s.top().second].dreapta = j - 1;
                s.pop();
            }
            if (!s.empty())
            {
                if (a[i][j] == a[s.top().first][s.top().second])
                    l[i][j].stanga = l[s.top().first][s.top().second].stanga;
                else
                    l[i][j].stanga = s.top().second + 1;
            }
            s.push({i, j});
        }
    }

    for (int j = 1; j <= n; ++j)
    {
        s = stack<pair<int, int>>();
        for (int i = 1; i <= n; ++i)
        {
            l[i][j].sus = 1;
            l[i][j].jos = n;
            while (!s.empty() && a[i][j] < a[s.top().first][s.top().second])
            {
                l[s.top().first][j].jos = i - 1;
                s.pop();
            }
            if (!s.empty())
            {
                if (a[i][j] == a[s.top().first][s.top().second])
                    l[i][j].sus = l[s.top().first][s.top().second].sus;
                else
                    l[i][j].sus = s.top().first + 1;
            }

            s.push({i, j});
        }
    }
}

long long solve1()
{
    long long total = 0;
    for (int i = 1; i <= n; ++i)
        for (int j = 1; j <= n; ++j)
        {
            total += (1LL * (i - l[i][j].sus + 1) * (j - l[i][j].stanga + 1) * (l[i][j].dreapta - j + 1) * (l[i][j].jos - i + 1)) % MOD;
            total %= MOD;
        }
    return total;
}

void computeSums()
{
    for (int i = 1; i <= n; ++i)
        for (int j = 1; j <= n; ++j)
        {
            spl[i][j] = (spl[i][j - 1] + a[i][j]) % MOD;
            sspl[i][j] = (sspl[i][j - 1] + spl[i][j]) % MOD;
            spc[i][j] = (spc[i - 1][j] + a[i][j]) % MOD;
            sspc[i][j] = (sspc[i - 1][j] + spc[i][j]) % MOD;
        }
}

long long solve2()
{
    computeSums();
    long long rez = 0;
    for (int i = 1; i <= n; ++i)
        for (int j = 1; j <= n; ++j)
        {
            long long valCrt = 0;
            // sr - suma pe ramura din dreapta
            // sl - suma pe ramura din stanga
            // su - suma pe ramura de sus
            // sd - suma pe ramura de jos
            long long sr = transform(1LL * sspl[i][l[i][j].dreapta] - sspl[i][j] - (1LL * ((l[i][j].dreapta - j) * spl[i][j]) % MOD)),

                      sd = transform(1LL * sspc[l[i][j].jos][j] - sspc[i][j] - ((1LL * (l[i][j].jos - i) * spc[i][j]) % MOD)),

                      sl = transform(1LL * (j - l[i][j].stanga + 1) * transform(spl[i][j - 1] - spl[i][l[i][j].stanga - 1]) -
                                     sspl[i][j - 1] + sspl[i][l[i][j].stanga - 1] + (1LL * (j - l[i][j].stanga) * spl[i][l[i][j].stanga - 1]) % MOD),

                      su = transform(1LL * (i - l[i][j].sus + 1) * transform(spc[i - 1][j] - spc[l[i][j].sus - 1][j]) -
                                     sspc[i - 1][j] + sspc[l[i][j].sus - 1][j] + 1LL * (i - l[i][j].sus) * spc[l[i][j].sus - 1][j] % MOD);

            // calculam numarul total de formatii care se pot forma cu cate 3 laturi selectate
            // cntURD - numarul de formatii care se pot forma cu laturile de sus, dreapta si jos
            // cntDRL - numarul de formatii care se pot forma cu laturile de jos, dreapta si stanga
            // cntLUR - numarul de formatii care se pot forma cu laturile de stanga, sus si dreapta
            // cntLUD - numarul de formatii care se pot forma cu laturile de stanga, sus si jos
            int cntURD = (1LL * (i - l[i][j].sus + 1) * (l[i][j].dreapta - j + 1) * (l[i][j].jos - i + 1)) % MOD,
                DRL = (1LL * (l[i][j].jos - i + 1) * (l[i][j].dreapta - j + 1) * (j - l[i][j].stanga + 1)) % MOD,
                cntLUR = (1LL * (j - l[i][j].stanga + 1) * (i - l[i][j].sus + 1) * (l[i][j].dreapta - j + 1)) % MOD,
                cntLUD = (1LL * (j - l[i][j].stanga + 1) * (i - l[i][j].sus + 1) * (l[i][j].jos - i + 1)) % MOD,
                cntToate = (1LL * (i - l[i][j].sus + 1) * (j - l[i][j].stanga + 1) * (l[i][j].dreapta - j + 1) * (l[i][j].jos - i + 1)) % MOD;

            valCrt = (1LL * sr * cntLUD) % MOD + (1LL * sd * cntLUR) % MOD + (1LL * sl * cntURD) % MOD + (1LL * su * DRL) % MOD + (1LL * a[i][j] * cntToate) % MOD;
            valCrt = transform(valCrt);

            rez = (rez + valCrt * a[i][j]) % MOD;
        }
    return rez;
}

long long solve()
{
    read();
    computeLimits();
    long long rez = 0;
    if (c == 1)
        rez = solve1();
    else if (c == 2)
        rez = solve2();
    return rez;
}
int main()
{
    fout << solve() << '\n';
    return 0;
}
```
