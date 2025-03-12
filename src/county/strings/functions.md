# Șiruri de caractere. Funcții specifice

## Funcții din `<string.h>`

În acest header, avem funcții special definite pentru caractere, care verifică diverse proprietăți ale acestora

- `isdigit` - verifică dacă un caracter este un număr
- `isalpha` - verifică dacă un caracter este o literă
- `islower` - verifică dacă un caracter este o literă mică
- `isupper` - verifică dacă un caracter este o literă mare
- `isspace` - verifică dacă un caracter este un spațiu
- `isalnum` - verifică dacă un caracter este o literă sau un număr

Pentru cuvintele reprezentate ca șiruri de caractere (`char[]`), există funcții în biblioteca `<string.h>` care permit operații specifice.

- `strlen` - returnează lungimea unui șir de caractere
  - când iterăm prin șir, putem folosi strlen ca și limită a buclei, dar putem și să ne folosim de faptul că ultimul caracter din șir este `'\0'` (`for (int i = 0; s[i]; i++)`)
- `strcpy` - copiază un șir de caractere în altul (complexitatea este $O(n)$ unde $n$ este lungimea șirului)
- `strcat` - concatenează două șiruri de caractere (complexitatea este $O(n)$ unde $n$ este lungimea șirului)
- `strcmp` - compară două șiruri de caractere (complexitatea este $O(n)$ unde $n$ este lungimea șirului)
- `strchr` - caută un caracter într-un șir de caractere (complexitatea este $O(n)$ unde $n$ este lungimea șirului)
- `strstr` - caută un subșir într-un șir de caractere (complexitatea este $O(n ^ 2)$ unde $n$ este lungimea șirului)

Pe lângă acestea, există funcții care lucrează direct cu memoria, cum ar fi `memset` și `memcpy`.

- `memset` - setează o zonă de memorie la o valoare dată. **ATENȚIE** funcționează cu numere în baza 16, adică `0x3F` înseamnă 63 în baza 10.

### Exemplu

```c
int s[100];
memset(s, 0, sizeof(s));
```

```cpp
const int oo = 0x3f3f3f3f; // un număr mare în baza 16
char s[100];
memset(s, oo, sizeof(s));
```

## Stringuri

Stringurile reprezintă o variantă mai variată și sigură a șirurilor de caractere. În general, funcțiile din `<algorithm>` se pot folosi pentru a lucra cu stringuri.

### Funcții relevante

- `std::string::find` - caută un subșir într-un șir
- `std::string::substr` - extrage un subșir dintr-un șir
- `std::string::insert` - inserează un subșir într-un șir
- `std::string::erase` - șterge un subșir dintr-un șir
- `std::string::replace` - înlocuiește un subșir cu altul
- `std::string::c_str` - returnează un pointer la șirul de caractere

### Exemplu

```cpp
std::string s = "Hello, world!";
std::string sub = s.substr(0, 5); // "Hello"
std::string sub2 = s.substr(7); // "world!"
```

```cpp
std::string s = "Hello, world!";
s.insert(5, " there"); // "Hello there, world!"
```

Citirea și scrierea se face în felul următor:

```cpp
std::string s;
std::cin >> s;
std::getline(std::cin, s); // citeste inclusiv spatiile
std::cout << s;
```

## Prelucrarea în tokenuri

Tokenurile sunt subșiruri care se formează în funcție de un separator.

### strtok

Funcția `strtok` este o funcție care împarte un șir de caractere în tokenuri în funcție de un separator, și returnează un pointer la fiecare token.

```cpp
char s[] = "Ana are mere si pere";
char *token = strtok(s, " ");

while (token != NULL) {
    std::cout << token << std::endl;
    token = strtok(NULL, " ");
}
```

### istringstream

Clasa `istringstream` este o clasă care permite citirea unui șir de caractere în funcție de un separator. Returnează un stream care poate fi citit ca orice alt stream. Folosită în special în combinație cu stringurile.

```cpp
std::string s = "Ana are mere si pere";
std::istringstream iss(s);
std::string token;

while (iss >> token) {
    std::cout << token << std::endl;
}
```

Putem și să definim un separator pentru `getline`:

```cpp
#include <iostream>
#include <string>
#include <sstream>

int main()
{
  std::istringstream iss { "Cpp|is|fun" };

  std::string s;
  while ( std::getline( iss, s, '|' ) ) // foloseste | ca si separator pentru getline
    std::cout << s << std::endl;

  return 0;
}
```
