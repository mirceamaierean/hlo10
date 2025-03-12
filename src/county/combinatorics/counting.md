# Formule de Numărare

## Numărul de submulțimi ale unei mulțimi

Numărul de submulțimi ale unei mulțimi \\(A\\) cu \\(n\\) elemente este egal cu \\(2^n\\).

## Permutări

### Permutări simple

Numărul de moduri în care putem aranja \\(n\\) elemente distincte:
\\[P_n = n!\\]

### Permutări cu repetiții

Numărul de moduri în care putem aranja \\(n\\) elemente, unde avem \\(k\\) tipuri de elemente
$$P(n_1, n_2, \dots, n_k) = \frac{n!}{n_1! \cdot n_2! \cdot \dots \cdot n_k!}$$ unde \\(n_1 + n_2 + \dots + n_k = n\\)

### Permutări cu puncte fixe

**Prof. DANIEL SITARU**

### Definiție

Fie permutarea \\( \sigma \\) definită pe mulțimea \\( \\{1, 2, \ldots, n\\} \\):

$$
\sigma = \begin{pmatrix}
1 & 2 & \ldots & n \\
\sigma(1) & \sigma(2) & \ldots & \sigma(n)
\end{pmatrix}
$$

Spunem că permutarea \\( \sigma \\) admite o coincidență în \\( i \in \\{1, 2, \ldots, n\\} \\) dacă \\( \sigma(i) = i \\). Numărul \\( i \\) cu această proprietate se numește **punct fix** al permutării \\( \sigma \\).

Prin \\( !n \\) (left factorial) vom nota numărul de permutări fără puncte fixe ale mulțimii \\( \\{1, 2, \ldots, n\\} \\).

Prima demonstrație a faptului că:

$$
\sum\_{k=0}^{n} \frac{(-1)^k}{k!} \cdot n! = !n
$$

a fost dată în 1713 de P.R. de Montmort și găsită independent de L. Euler în 1753.

#### Proprietatea 1

$$
\sum\_{k=0}^{n} \frac{(-1)^k}{k!} \cdot n! = !n
$$

#### Proprietatea 2

Pentru orice \\( n \in \mathbb{N} \\), avem: \\(!n = n \cdot !(n - 1) + (-1) ^ n\\)

#### Proprietatea 3

Pentru orice \\( n \geq 2 \\), avem: \\(!n = (n - 1) \cdot [!(n - 1) + !(n - 2)]\\)

## Aranjamente

Numărul de moduri în care putem selecta și aranja \\(k\\) elemente din \\(n\\) elemente distincte:
\\[A_n^k = \frac{n!}{(n-k)!} = n \cdot (n-1) \cdot \ldots \cdot (n-k+1)\\]

## Combinări

Numărul de moduri în care putem selecta \\(k\\) elemente din \\(n\\) elemente distincte (ordinea nu contează):
\\[C_n^k = \binom{n}{k} = \frac{n!}{k!(n-k)!}\\]

## Proprietăți importante

### Proprietăți ale combinărilor

1. \\(\binom{n}{k} = \binom{n}{n-k}\\)
2. \\(\binom{n}{k} = \binom{n-1}{k} + \binom{n-1}{k-1}\\) (Formula lui Pascal)
3. \\(\sum\_{k=0}^n \binom{n}{k} = 2^n\\)
4. \\(\binom{n}{0} + \binom{n}{1} + \dots + \binom{n}{n} = 2^n\\)
5. \\(\binom{n}{0}^2 + \binom{n}{1}^2 + \dots + \binom{n}{n}^2 = \binom{2n}{n}\\)

## Principii de numărare

### Principiul adunării

Dacă o acțiune se poate realiza în \\(n\\) moduri, iar o altă acțiune se poate realiza în \\(m\\) moduri, și cele două acțiuni nu pot fi realizate simultan, atunci una din cele două acțiuni se poate realiza în \\(n + m\\) moduri.

### Principiul înmulțirii

Dacă o acțiune se poate realiza în \\(n\\) moduri, iar după aceasta o altă acțiune se poate realiza în \\(m\\) moduri, atunci succesiunea celor două acțiuni se poate realiza în \\(n \cdot m\\) moduri.

### Principiul includerii și excluderii

Pentru două mulțimi:
\\[|A \cup B| = |A| + |B| - |A \cap B|\\]

Pentru trei mulțimi:
\\[|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|\\]

Formula generală pentru \\(n\\) mulțimi:
\\[|\bigcup_{i=1}^n A_i| = \sum_{k=1}^n (-1)^{k-1} \sum_{1 \leq i_1 < i_2 < \dots < i_k \leq n} |A_{i_1} \cap A_{i_2} \cap \dots \cap A_{i_k}|\\]

### Numărul de partiții ale unui număr

#### Definiție

Numim partiție a lui \\(n \in \mathbb{N}\\) o secvență de numere naturale nenule \\(P = \langle p_1, p_2, \ldots, p_k \rangle\\) cu proprietatea că \\(p_1 + p_2 + \cdots + p_k = n\\). Dacă secvența \\(P\\) este ordonată, partiția este ordonată, iar în caz contrar, neordonată.

#### Exemple

Pentru \\(n = 4\\), partițiile ordonate sunt:
\\[(1, 1, 1, 1), (1, 1, 2), (1, 2, 1), (1, 3), (2, 1, 1), (2, 2), (3, 1), (4)\\]

Partițiile neordonate ale lui 4 sunt:
\\[[1, 1, 1, 1], [1, 1, 2], [1, 3], [2, 2], [4]\\]

Observăm că partițiile ordonate \\((1, 1, 2)\\) și \\((1, 2, 1)\\) sunt diferite, pe când partițiile neordonate \\([1, 1, 2]\\) și \\([1, 2, 1]\\) sunt egale.

#### Convenție

Prin convenție, numărul de partiții ale lui 0 este 1. Convenția este justificată, deoarece putem considera că mulțimea vidă este o partiție a lui 0, suma elementelor ei fiind 0.

#### Numărul de partiții ordonate

Fie \\(p(n, k)\\) numărul de partiții ordonate ale lui \\(n\\), de lungime \\(k\\). Pentru a număra partițiile ordonate, putem reduce problema la una mai ușor de abordat:

**Problema echivalentă**: Să se determine numărul modurilor de a împărți un șir de lungime \\(n\\) în \\(k\\) secvențe de lungimi nenule.

De exemplu, șirul `xxxxx` poate fi împărțit în 3 secvențe astfel:

```
x x xxx
x xx xx
x xxx x
xx x xx
xx xx x
xxx x x
```

Este clar că o astfel de împărțire a unui șir este de fapt o partiție a lui \\(n\\), în care lungimea fiecărei secvențe reprezintă valoarea unui element din partiție.

Practic, trebuie să găsim numărul de moduri de a alege cele \\(k - 1\\) puncte de split, adică acele poziții pe care se termină fiecare secvență, mai puțin ultima (pentru că ea are poziția de sfârșit fixată). Aceste poziții iau valori din mulțimea \\(\\{1, 2, \ldots, n-1\\}\\). Cum ele trebuie să fie distincte, se observă ușor că soluția e dată de \\(C\_{n-1}^{k-1}\\).

Acum, dacă vrem să calculăm numărul total de partiții ordonate ale lui \\(n\\), nu avem decât să însumăm niște combinări. Mai exact, dacă notăm cu \\(p(n)\\) numărul tuturor partițiilor ordonate ale lui \\(n\\), obținem:

\\[p(n) = C_{n-1}^0 + C_{n-1}^1 + \cdots + C_{n-1}^{n-1} = 2^{n-1}\\]

# Numerele lui Catalan

Numerele catalane reprezintă o secvență de numere, care se dovedește a fi utilă într-o serie de probleme combinatorii, care implică adesea obiecte definite recursiv.

Această secvență a fost numită după matematicianul belgian Catalan, care a trăit în secolul al XIX-lea. (De fapt, ea a fost cunoscută înaintea lui Euler, care a trăit cu un secol înaintea lui Catalan).

## Primele numere catalane

Primele numere catalane sunt (\\(C_n\\) și n începând de la 0):

\\[1, 1, 2, 5, 14, 42, 132, 429, 1430, \ldots\\]

## Aplicații în unele probleme de combinatorica

Numărul catalan \\(C_n\\) este soluția pentru:

1. Numărul de secvențe de paranteze corecte formate din n paranteze de deschise și n paranteze de închise.

2. Numărul de arbori binari cu rădăcina și n+1 frunze (vârfurile nu sunt numerotate). Un arbore binar înrădăcinat este complet dacă fiecare vârf are fie doi copii, fie niciun copil.

3. Numărul de moduri de a pune complet între paranteze n+1 factori.

4. Numărul de triangulații ale unui poligon convex cu n+2 laturi (adică numărul de împărțiri ale poligonului în triunghiuri disjuncte prin utilizarea diagonalelor).

5. Numărul de moduri în care se pot lega cele 2n puncte de pe un cerc pentru a forma n coarde disjuncte.

6. Numărul de arbori binari compleți neizomorfi cu n noduri interne (adică noduri care au cel puțin un fiu).

7. Numărul de trasee monotone de rețea de la punctul (0, 0) la punctul (n, n) într-o rețea pătrată de dimensiune nxn, care nu trec deasupra diagonalei principale (adică (0, 0) care face legătura cu (n, n)).

8. Numărul de permutări de lungime n care pot fi ordonate în stivă (adică se poate demonstra că rearanjarea este ordonată în stivă dacă și numai dacă nu există un astfel de indice i<j<k, astfel încât \\(a_k < a_i < a_j\\)).

9. Numărul de partiții neîncrucișate ale unui set de n elemente.

10. Numărul de moduri în care se poate acoperi scara \\(1 \ldots n\\) folosind n dreptunghiuri (scara este formată din n coloane, unde coloana are înălțimea i).

## Mod de calcul

Există două formule pentru numerele catalane: Recursivă și Analitică. Deoarece considerăm că toate problemele menționate mai sus sunt echivalente (au aceeași soluție), pentru demonstrarea formulelor de mai jos vom alege sarcina care este cel mai ușor de realizat.

### Formulă recurentă

\\[C_0 = C_1 = 1\\]
\\[C_n = \sum_{k=0}^{n-1} C_k C_{n-1-k}, n \geq 2\\]

Formula de recurență poate fi dedusă cu ușurință din problema secvenței corecte de paranteze.

Cea mai din stânga paranteză de deschidere l corespunde unei anumite paranteze de închidere r, care împarte secvența în 2 părți care, la rândul lor, ar trebui să fie o secvență corectă de paranteze. Astfel, formula este, de asemenea, împărțită în 2 părți. Dacă notăm \\(k = r-l-1\\), atunci, pentru un r fix, vor exista exact \\(C*k C*{n-1-k}\\) astfel de secvențe de paranteze. Însumând acest lucru peste toate \\(k\\)'s admisibile, obținem relația de recurență pe \\(C_n\\).

De asemenea, puteți gândi în felul următor. Prin definiție, \\(C_n\\) reprezintă numărul de secvențe de paranteze corecte. Acum, secvența poate fi împărțită în 2 părți de lungime k și n-k, fiecare dintre acestea trebuind să fie o secvență corectă de paranteze. Exemplu:

\\(()((()))\\) poate fi împărțit în \\(()\\) și \\((()))\\), dar nu poate fi împărțit în \\(()\\) și \\(()\\). Însumând din nou peste toate \\(k\\)'s admisibile, obținem relația de recurență pe \\(C_n\\).

```cpp
const int MOD = ....
const int MAX = ....
int catalan[MAX];
void init() {
    catalan[0] = catalan[1] = 1;
    for (int i=2; i<=n; i++) {
        catalan[i] = 0;
        for (int j=0; j < i; j++) {
            catalan[i] += (catalan[j] * catalan[i-j-1]) % MOD;
            if (catalan[i] >= MOD) {
                catalan[i] -= MOD;
            }
        }
    }
}
```

### Formula analitică

\\[C_n = \frac{1}{n+1}\binom{2n}{n}\\]

(aici \\(\binom{n}{k}\\) reprezintă coeficientul binomial obișnuit, adică numărul de moduri de a selecta k obiecte dintr-un set de n obiecte).

Formula de mai sus poate fi ușor de concluzionat din problema traseelor monotone în rețeaua pătrată. Numărul total de trasee monotone în rețeaua de dimensiuni nxn este dat de \\(\binom{2n}{n}\\)

Acum numărăm numărul de trasee monotone care traversează diagonala principală. Considerăm astfel de traiectorii care traversează diagonala principală și găsim prima muchie din ea care se află deasupra diagonalei. Reflectăm traiectoria în jurul diagonalei până la capăt, mergând după această muchie. Rezultatul este întotdeauna o traiectorie monotonă în grila (n-1) × (n+1). Pe de altă parte, orice traiectorie monotonă în grila (n-1) × (n+1) trebuie să intersecteze diagonala. Prin urmare, am enumerat toate căile monotone care intersectează diagonala principală în rețeaua n x n.

Numărul de drumuri monotone în rețeaua (n-1) × (n+1) este \\(\binom{2n}{n-1}\\). Numim astfel de trasee "rele". Ca urmare, pentru a obține numărul de trasee monotone care nu traversează diagonala principală, scădem traseele "rele" de mai sus, obținând formula:

\\[C_n = \binom{2n}{n} - \binom{2n}{n-1} = \frac{1}{n+1}\binom{2n}{n}, n \geq 0\\]

## Referințe:

- http://www.geometer.org/mathcircles/catalan.pdf
