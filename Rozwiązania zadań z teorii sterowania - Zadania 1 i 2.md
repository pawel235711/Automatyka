# Rozwiązania zadań z teorii sterowania - Zadania 1 i 2

## Zadanie 1: Wyznaczanie macierzy w przestrzeni stanu

### Treść zadania

Mamy dane dwie transmitancje:

**Transmitancja 1:**
```
G(s) = (s² + 6s + 10) / (s⁵ - 3s⁴ + 3s³ - 3s² - 8s + 11)
```

**Transmitancja 2:**
```
Ĝ(s) = 3s² / (s⁵ - 2s⁴ - 12s³ - 3s² + s + 11)
```

**Zadanie:** Wyznaczyć macierze **A**, **B**, **C**, **D** w przestrzeni stanu dla obu transmitancji.

---

### Co to jest przestrzeń stanu?

**Przestrzeń stanu** to sposób opisu układu dynamicznego za pomocą równań różniczkowych pierwszego rzędu. Zamiast operować na transmitancji (która jest w dziedzinie operatorowej), opisujemy układ za pomocą **zmiennych stanu**.

Układ w przestrzeni stanu ma postać:

```
dx/dt = Ax + Bu    (równanie stanu)
y = Cx + Du        (równanie wyjścia)
```

gdzie:
- **x** - wektor zmiennych stanu (wektor n×1)
- **u** - sygnał wejściowy (skalar lub wektor)
- **y** - sygnał wyjściowy (skalar lub wektor)
- **A** - macierz stanu (n×n)
- **B** - macierz wejścia (n×1)
- **C** - macierz wyjścia (1×n)
- **D** - macierz przejścia bezpośredniego (skalar)

---

### Jak przekształcić transmitancję do przestrzeni stanu?

Transmitancja ma postać:

```
G(s) = Y(s)/U(s) = (b_m·s^m + b_(m-1)·s^(m-1) + ... + b_1·s + b_0) / (s^n + a_(n-1)·s^(n-1) + ... + a_1·s + a_0)
```

Istnieje kilka postaci kanonicznych (sposobów zapisu). Najczęściej używana to **postać kanoniczna sterowania** (controllable canonical form).

---

### Rozwiązanie dla transmitancji G(s)

#### Krok 1: Zapisanie transmitancji w postaci standardowej

```
G(s) = (s² + 6s + 10) / (s⁵ - 3s⁴ + 3s³ - 3s² - 8s + 11)
```

Licznik:
```
N(s) = s² + 6s + 10
Współczynniki: b₂ = 1, b₁ = 6, b₀ = 10
```

Mianownik:
```
D(s) = s⁵ - 3s⁴ + 3s³ - 3s² - 8s + 11
Współczynniki: a₄ = -3, a₃ = 3, a₂ = -3, a₁ = -8, a₀ = 11
```

Rząd układu: **n = 5** (najwyższa potęga mianownika)

#### Krok 2: Postać kanoniczna sterowania

W postaci kanonicznej sterowania macierze mają następującą strukturę:

**Macierz A** (5×5):
```
     ⎡  0      1      0      0      0  ⎤
     ⎢  0      0      1      0      0  ⎥
A =  ⎢  0      0      0      1      0  ⎥
     ⎢  0      0      0      0      1  ⎥
     ⎣ -a₀   -a₁    -a₂    -a₃    -a₄ ⎦
```

Podstawiając współczynniki z mianownika:
```
     ⎡  0      1      0      0      0  ⎤
     ⎢  0      0      1      0      0  ⎥
A =  ⎢  0      0      0      1      0  ⎥
     ⎢  0      0      0      0      1  ⎥
     ⎣-11      8     -3     -3      3  ⎦
```

**Wyjaśnienie:** 
- Ostatni wiersz zawiera współczynniki mianownika ze znakiem przeciwnym (oprócz współczynnika przy s⁵, który jest równy 1)
- Reszta macierzy tworzy łańcuch integratorów (same 1 na naddiagonali)

**Macierz B** (5×1):
```
     ⎡ 0 ⎤
     ⎢ 0 ⎥
B =  ⎢ 0 ⎥
     ⎢ 0 ⎥
     ⎣ 1 ⎦
```

**Wyjaśnienie:** Sygnał wejściowy wpływa tylko na ostatnią zmienną stanu.

**Macierz C** (1×5):

Tutaj musimy uwzględnić współczynniki licznika. Ponieważ licznik ma stopień 2 (s²), a mianownik stopień 5, mamy:

```
C = [b₀  b₁  b₂  0  0] = [10  6  1  0  0]
```

**Wyjaśnienie:** Współczynniki licznika zapisujemy od najmniejszej potęgi. Brakujące współczynniki (dla s³ i s⁴) uzupełniamy zerami.

**Macierz D** (skalar):
```
D = 0
```

**Wyjaśnienie:** Nie ma bezpośredniego przejścia z wejścia na wyjście, ponieważ stopień licznika jest mniejszy niż stopień mianownika.

---

### Rozwiązanie dla transmitancji Ĝ(s)

#### Krok 1: Zapisanie transmitancji w postaci standardowej

```
Ĝ(s) = 3s² / (s⁵ - 2s⁴ - 12s³ - 3s² + s + 11)
```

Licznik:
```
N(s) = 3s²
Współczynniki: b₂ = 3, b₁ = 0, b₀ = 0
```

Mianownik:
```
D(s) = s⁵ - 2s⁴ - 12s³ - 3s² + s + 11
Współczynniki: a₄ = -2, a₃ = -12, a₂ = -3, a₁ = 1, a₀ = 11
```

Rząd układu: **n = 5**

#### Krok 2: Postać kanoniczna sterowania

**Macierz A** (5×5):
```
     ⎡  0      1      0      0      0  ⎤
     ⎢  0      0      1      0      0  ⎥
A =  ⎢  0      0      0      1      0  ⎥
     ⎢  0      0      0      0      1  ⎥
     ⎣-11     -1      3     12      2  ⎦
```

**Wyjaśnienie:** Ostatni wiersz: [-a₀, -a₁, -a₂, -a₃, -a₄] = [-11, -1, 3, 12, 2]

**Macierz B** (5×1):
```
     ⎡ 0 ⎤
     ⎢ 0 ⎥
B =  ⎢ 0 ⎥
     ⎢ 0 ⎥
     ⎣ 1 ⎦
```

**Macierz C** (1×5):
```
C = [0  0  3  0  0]
```

**Wyjaśnienie:** Współczynnik przy s² wynosi 3, więc umieszczamy go na trzeciej pozycji (odpowiadającej s²).

**Macierz D** (skalar):
```
D = 0
```

---

### Podsumowanie wyników dla Zadania 1

#### Dla G(s):

**Macierz A:**
```
⎡  0   1   0   0   0 ⎤
⎢  0   0   1   0   0 ⎥
⎢  0   0   0   1   0 ⎥
⎢  0   0   0   0   1 ⎥
⎣-11   8  -3  -3   3 ⎦
```

**Macierz B:**
```
⎡ 0 ⎤
⎢ 0 ⎥
⎢ 0 ⎥
⎢ 0 ⎥
⎣ 1 ⎦
```

**Macierz C:**
```
[10  6  1  0  0]
```

**Macierz D:**
```
0
```

#### Dla Ĝ(s):

**Macierz A:**
```
⎡  0   1   0   0   0 ⎤
⎢  0   0   1   0   0 ⎥
⎢  0   0   0   1   0 ⎥
⎢  0   0   0   0   1 ⎥
⎣-11  -1   3  12   2 ⎦
```

**Macierz B:**
```
⎡ 0 ⎤
⎢ 0 ⎥
⎢ 0 ⎥
⎢ 0 ⎥
⎣ 1 ⎦
```

**Macierz C:**
```
[0  0  3  0  0]
```

**Macierz D:**
```
0
```

---


## Zadanie 2: Wyznaczanie transmitancji operatorowej z modelu w przestrzeni stanu

### Treść zadania

Mamy dany model w przestrzeni stanu:

**Macierz A:**
```
⎡ 3  1   5 ⎤
⎢-3  0  -1 ⎥
⎣ 1  3  -2 ⎦
```

**Macierz B:**
```
⎡ 2 ⎤
⎢ 1 ⎥
⎣ 3 ⎦
```

**Macierz C:**
```
[0  2  3]
```

**Macierz D:**
```
[4]
```

**Zadanie:** Wyznaczyć transmitancję operatorową G(s).

---

### Jak przekształcić przestrzeń stanu do transmitancji?

Transmitancję G(s) z modelu w przestrzeni stanu obliczamy ze wzoru:

```
G(s) = C · [sI - A]⁻¹ · B + D
```

gdzie:
- **I** - macierz jednostkowa (o takich samych wymiarach jak A)
- **[sI - A]⁻¹** - macierz odwrotna do macierzy (sI - A)

---

### Rozwiązanie krok po kroku

#### Krok 1: Obliczenie macierzy (sI - A)

```
sI - A = s · ⎡ 1  0  0 ⎤ - ⎡ 3  1   5 ⎤
             ⎢ 0  1  0 ⎥   ⎢-3  0  -1 ⎥
             ⎣ 0  0  1 ⎦   ⎣ 1  3  -2 ⎦

       = ⎡ s  0  0 ⎤ - ⎡ 3  1   5 ⎤
         ⎢ 0  s  0 ⎥   ⎢-3  0  -1 ⎥
         ⎣ 0  0  s ⎦   ⎣ 1  3  -2 ⎦

       = ⎡ s-3  -1   -5  ⎤
         ⎢  3    s    1  ⎥
         ⎣ -1   -3   s+2 ⎦
```

#### Krok 2: Obliczenie wyznacznika macierzy (sI - A)

Wyznacznik `det(sI - A)` obliczymy metodą Sarrusa:

```
det(sI - A) = (s-3)·s·(s+2) + (-1)·1·(-1) + (-5)·3·(-3) - [(-5)·s·(-1) + (-1)·3·(s+2) + (s-3)·1·(-3)]

            = (s²-3s)(s+2) + 1 + 45 - [5s - 3(s+2) - 3(s-3)]

            = s³ + 2s² - 3s² - 6s + 46 - [5s - 3s - 6 - 3s + 9]

            = s³ - s² - 6s + 46 - [-s + 3]

            = s³ - s² - 6s + 46 + s - 3

            = s³ - s² - 5s + 43
```

Wyznacznik jest mianownikiem naszej transmitancji.

#### Krok 3: Obliczenie macierzy odwrotnej [sI - A]⁻¹

Macierz odwrotna to `(1/det) · adj(A)`, gdzie `adj(A)` to macierz dołączona (transponowana macierz dopełnień algebraicznych).

```
adj(sI - A) = ⎡ C₁₁  C₂₁  C₃₁ ⎤
              ⎢ C₁₂  C₂₂  C₃₂ ⎥
              ⎣ C₁₃  C₂₃  C₃₃ ⎦
```

Obliczamy poszczególne dopełnienia algebraiczne:

```
C₁₁ = +(s·(s+2) - 1·(-3)) = s² + 2s + 3
C₁₂ = -(3·(s+2) - 1·(-1)) = -(3s + 6 + 1) = -3s - 7
C₁₃ = +(3·(-3) - s·(-1)) = -9 + s

C₂₁ = -((-1)·(s+2) - (-5)·(-3)) = -(-s - 2 - 15) = s + 17
C₂₂ = +((s-3)·(s+2) - (-5)·(-1)) = s² - s - 6 - 5 = s² - s - 11
C₂₃ = -((s-3)·(-3) - (-1)·(-1)) = -(-3s + 9 - 1) = 3s - 8

C₃₁ = +((-1)·1 - (-5)·s) = 5s - 1
C₃₂ = -((s-3)·1 - (-5)·3) = -(s - 3 + 15) = -s - 12
C₃₃ = +((s-3)·s - (-1)·3) = s² - 3s + 3
```

Macierz dołączona (transponowana):
```
adj(sI - A) = ⎡ s²+2s+3    s+17      5s-1   ⎤
              ⎢ -3s-7     s²-s-11   -s-12  ⎥
              ⎣  s-9       3s-8     s²-3s+3 ⎦
```

#### Krok 4: Obliczenie iloczynu C · adj(sI - A) · B

Najpierw obliczymy `adj(sI - A) · B`:

```
⎡ s²+2s+3    s+17      5s-1   ⎤   ⎡ 2 ⎤   ⎡ 2(s²+2s+3) + 1(s+17) + 3(5s-1)   ⎤
⎢ -3s-7     s²-s-11   -s-12  ⎥ · ⎢ 1 ⎥ = ⎢ 2(-3s-7) + 1(s²-s-11) + 3(-s-12)  ⎥
⎣  s-9       3s-8     s²-3s+3 ⎦   ⎣ 3 ⎦   ⎣ 2(s-9) + 1(3s-8) + 3(s²-3s+3)    ⎦

= ⎡ 2s²+4s+6 + s+17 + 15s-3 ⎤   ⎡ 2s² + 20s + 20 ⎤
  ⎢ -6s-14 + s²-s-11 -3s-36 ⎥ = ⎢ s² - 10s - 61  ⎥
  ⎣ 2s-18 + 3s-8 + 3s²-9s+9  ⎦   ⎣ 3s² - 4s - 17  ⎦
```

Teraz mnożymy wynik przez `C`:

```
C · [adj(sI - A) · B] = [0  2  3] · ⎡ 2s² + 20s + 20 ⎤
                                  ⎢ s² - 10s - 61  ⎥
                                  ⎣ 3s² - 4s - 17  ⎦

= 0·(2s² + 20s + 20) + 2·(s² - 10s - 61) + 3·(3s² - 4s - 17)

= 2s² - 20s - 122 + 9s² - 12s - 51

= 11s² - 32s - 173
```

To jest licznik naszej transmitancji (część ułamkowa).

#### Krok 5: Złożenie końcowej transmitancji G(s)

```
G(s) = (C · adj(sI - A) · B) / det(sI - A) + D

G(s) = (11s² - 32s - 173) / (s³ - s² - 5s + 43) + 4
```

Aby uzyskać jeden ułamek, sprowadzamy do wspólnego mianownika:

```
G(s) = (11s² - 32s - 173 + 4·(s³ - s² - 5s + 43)) / (s³ - s² - 5s + 43)

G(s) = (11s² - 32s - 173 + 4s³ - 4s² - 20s + 172) / (s³ - s² - 5s + 43)

G(s) = (4s³ + 7s² - 52s - 1) / (s³ - s² - 5s + 43)
```

---

### Podsumowanie wyniku dla Zadania 2

Transmitancja operatorowa dla podanego modelu w przestrzeni stanu wynosi:

```
G(s) = (4s³ + 7s² - 52s - 1) / (s³ - s² - 5s + 43)
```


---

## Podsumowanie i wskazówki praktyczne

### Kluczowe wzory do zapamiętania

#### 1. Przekształcenie transmitancji do przestrzeni stanu (postać kanoniczna sterowania)

Dla transmitancji:
```
G(s) = (b_m·s^m + ... + b₁·s + b₀) / (s^n + a_(n-1)·s^(n-1) + ... + a₁·s + a₀)
```

Macierze:
```
     ⎡  0      1      0    ...   0  ⎤
     ⎢  0      0      1    ...   0  ⎥
A =  ⎢  ⋮      ⋮      ⋮     ⋱    ⋮  ⎥
     ⎢  0      0      0    ...   1  ⎥
     ⎣ -a₀   -a₁    -a₂   ... -a_(n-1) ⎦

     ⎡ 0 ⎤
     ⎢ 0 ⎥
B =  ⎢ ⋮ ⎥
     ⎢ 0 ⎥
     ⎣ 1 ⎦

C = [b₀  b₁  b₂  ...  b_m  0  ...  0]

D = 0  (jeśli stopień licznika < stopień mianownika)
```

#### 2. Przekształcenie przestrzeni stanu do transmitancji

```
G(s) = C · [sI - A]⁻¹ · B + D
```

Gdzie:
- `[sI - A]⁻¹ = adj(sI - A) / det(sI - A)`
- Licznik transmitancji: `C · adj(sI - A) · B + D · det(sI - A)`
- Mianownik transmitancji: `det(sI - A)`

---

### Najczęstsze błędy i jak ich unikać

#### Błąd 1: Nieprawidłowe znaki w macierzy A

**Uwaga:** W ostatnim wierszu macierzy A wpisujemy współczynniki mianownika **ze znakiem przeciwnym**.

Przykład: Jeśli mianownik to `s³ + 2s² - 5s + 3`, to ostatni wiersz A to `[-3, 5, -2]`.

#### Błąd 2: Nieprawidłowa kolejność współczynników w macierzy C

**Uwaga:** Współczynniki licznika w macierzy C wpisujemy **od najmniejszej potęgi** (b₀, b₁, b₂, ...).

Przykład: Jeśli licznik to `3s² + 2s + 1`, to C = `[1, 2, 3, 0, ...]`.

#### Błąd 3: Pomyłki w obliczaniu wyznacznika

**Wskazówka:** Przy obliczaniu wyznacznika macierzy 3×3 użyj metody Sarrusa lub rozwinięcia Laplace'a. Sprawdź obliczenia dwukrotnie.

#### Błąd 4: Zapomnienie o macierzy D

**Uwaga:** Jeśli D ≠ 0, pamiętaj o dodaniu `D · det(sI - A)` do licznika końcowej transmitancji.

---

### Weryfikacja wyników

Aby sprawdzić poprawność obliczeń, możesz:

1. **Sprawdzić wymiary macierzy:**
   - A: n×n
   - B: n×1
   - C: 1×n
   - D: skalar

2. **Sprawdzić rząd układu:**
   - Rząd układu = stopień mianownika transmitancji = wymiar macierzy A

3. **Użyć narzędzi komputerowych:**
   - MATLAB: funkcje `tf2ss()` i `ss2tf()`
   - Python: biblioteka `scipy.signal` z funkcjami `tf2ss()` i `ss2tf()`

---

### Przykład weryfikacji w Pythonie

```python
import numpy as np
from scipy.signal import ss2tf

# Zadanie 2 - weryfikacja
A = np.array([[3, 1, 5], [-3, 0, -1], [1, 3, -2]])
B = np.array([[2], [1], [3]])
C = np.array([[0, 2, 3]])
D = np.array([[4]])

# Obliczenie transmitancji
num, den = ss2tf(A, B, C, D)
print("Licznik:", num)
print("Mianownik:", den)
```

---

### Dodatkowe materiały

Jeśli chcesz pogłębić swoją wiedzę na temat teorii sterowania, polecam:

1. **Książki:**
   - "Teoria sterowania w zadaniach" - Kaczorek T.
   - "Podstawy automatyki" - Kasprzyk J.

2. **Kursy online:**
   - MIT OpenCourseWare: "Signals and Systems"
   - Coursera: "Control of Mobile Robots"

3. **Narzędzia:**
   - MATLAB Control System Toolbox
   - Python: biblioteki `control`, `scipy.signal`

---

## Autor

Rozwiązania przygotowane przez **Manus AI** - szczegółowe wyjaśnienia dla początkujących w teorii sterowania.

---

**Data:** 2 lutego 2026

**Format:** Markdown (kompatybilny z GitHub)
