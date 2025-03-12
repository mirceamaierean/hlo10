# Aritmetică Modulară

## Definiții și Concepte de Bază

### Congruență

Două numere întregi \\(a\\) și \\(b\\) sunt congruente modulo \\(n\\) dacă diferența lor este divizibilă cu \\(n\\). Notăm:
\\[a \equiv b \pmod{n}\\]

Echivalent, \\(a\\) și \\(b\\) sunt congruente modulo \\(n\\) dacă au același rest la împărțirea cu \\(n\\).

### Proprietăți ale Congruențelor

1. **Reflexivitate**: \\(a \equiv a \pmod{n}\\)
2. **Simetrie**: Dacă \\(a \equiv b \pmod{n}\\), atunci \\(b \equiv a \pmod{n}\\)
3. **Tranzitivitate**: Dacă \\(a \equiv b \pmod{n}\\) și \\(b \equiv c \pmod{n}\\), atunci \\(a \equiv c \pmod{n}\\)

### Operații cu Congruențe

Pentru orice \\(a_1 \equiv b_1 \pmod{n}\\) și \\(a_2 \equiv b_2 \pmod{n}\\), avem:

1. **Adunare**: \\(a_1 + a_2 \equiv b_1 + b_2 \pmod{n}\\)
2. **Scădere**: \\(a_1 - a_2 \equiv b_1 - b_2 \pmod{n}\\)
3. **Înmulțire**: \\(a_1 \cdot a_2 \equiv b_1 \cdot b_2 \pmod{n}\\)

### Proprietăți:

1. \\((a + b) \pmod{n} = (a \pmod{n} + b \pmod{n}) \pmod{n}\\)
2. \\((a - b) \pmod{n} = (a \pmod{n} - b \pmod{n} + n) \pmod{n}\\)
3. \\((a \cdot b) \pmod{n} = (a \pmod{n} \cdot b \pmod{n}) \pmod{n}\\)

### Invers Modular

#### Definiție

Pentru un număr \\(A\\) și un modul \\(N\\), inversul modular al lui \\(A\\) este un număr \\(X\\) astfel încât:
\\[A \cdot X \equiv 1 \pmod{N}\\]

#### Cum determinăm inversul modular?

Soluția optimă se obține folosind teorema lui Euler, din care avem că \\(A^{\varphi(N)} \equiv 1 \pmod{N}\\), unde \\(\varphi(N)\\) reprezintă numărul numerelor mai mici decât \\(N\\) și prime cu \\(N\\). Cum \\(A^{\varphi(N)} = A \cdot A^{\varphi(N)-1}\\) rezultă că \\(A^{\varphi(N)-1}\\) este inversul modular al lui \\(A\\). Soluția problemei va fi deci \\(A^{\varphi(N)-1} \bmod N\\). Putem folosi exponențierea în timp logaritmic pentru a calcula această putere în complexitate \\(O(\log N)\\).

În plus, putem calcula \\(\varphi(N)\\) în complexitate \\(O(\sqrt{N})\\). Pentru cazul particular când \\(N\\) este prim, \\(\varphi(N) = N - 1\\), deci răspunsul va fi \\(A^{N-2}\\).

```cpp
#include <iostream>
#include <fstream>

using namespace std;

ifstream fin("inversmodular.in");
ofstream fout("inversmodular.out");

long long eul(long long n)
{
    long long d = 2;
    long long cnd = n;
    while (n > 1)
    {
        if (n % d == 0)
        {
            cnd /= d;
            cnd *= (d - 1);
            while (n % d == 0)
                n /= d;
        }
        d++;
        if (d * d > n)
            d = n;
    }
    return cnd;
}

long long exp(long long eul, long long n, long long modulo)
{
    long long rest = 1;
    while (eul)
    {
        if (eul % 2 == 1)
        {
            rest *= n;
            rest %= modulo;
        }
        n *= n;
        n %= modulo;
        eul /= 2;
    }
    return rest;
}

int main()
{
    long long A, N, X;
    fin >> A >> N;
    long long e = eul(N);
    fout << exp(e - 1, A, N);
    return 0;
}
```

#### Aplicații

O aplicație foarte utilă a inversilor modulari este calcularea combinărilor, modulo un număr prim P dat. De exemplu, avem:

\\[C_N^K = \frac{N!}{K!(N-K)!} = N! \cdot (K!)^{-1} \cdot [(N-K)!]^{-1}\\]

Prin \\((K!)^{-1}\\) și \\([(N-K)!]^{-1}\\) se înțeleg inversii modulari ai acestor numere, modulo P. Astfel putem calcula o combinare de ordin N, modulo P, în timp \\(O(N)\\).

```cpp
// Calculul combinărilor modulo P

long long putere(long long b, int e)
{
    long long r = 1;
    while (e)
    {
        if (e & 1)
        {
            r *= b;
            r %= MOD;
        }
        b *= b;
        b %= MOD;
        e >>= 1;
    }
    return r;
}

void fact()
{
    f[0] = 1;
    for (int i = 1; i < NMAX; ++i)
    {
        f[i] = (1LL * f[i - 1] * i) % MOD;
    }
}

long long comb(long long n, long long k)
{
    if (n < 0 || k < 0 || n < k)
    {
        return 0;
    }
    return (((1LL * f[n] * putere(f[k], MOD - 2)) % MOD) * putere(f[n - k], MOD - 2)) % MOD;
}

```

Această metodă este deosebit de utilă în probleme care necesită calculul unui număr mare de combinări modulo un număr prim.


