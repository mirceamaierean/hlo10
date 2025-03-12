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
