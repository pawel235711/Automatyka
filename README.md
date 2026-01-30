# Tutorial z Automatyki dla Początkujących

## CZĘŚĆ I: PODSTAWY TEORETYCZNE

### 1. Wprowadzenie do teorii sterowania

Teoria sterowania to dziedzina inżynierii i matematyki, która zajmuje się modelowaniem, analizą i regulacją obiektów dynamicznych. Celem jest wpłynięcie na zachowanie obiektu w taki sposób, aby osiągnąć pożądany stan lub trajektorię.

**Podstawowe pojęcia:**

*   **Układ sterowania:** Zespół połączonych ze sobą elementów, którego celem jest sterowanie określonym obiektem. Składa się z obiektu sterowania, urządzenia sterującego (regulatora) oraz czujników pomiarowych.
*   **Sygnał wejściowy (sterujący):** Sygnał podawany na wejście układu, który ma na celu wymuszenie określonego zachowania. Oznaczany jako `u(t)`.
*   **Sygnał wyjściowy (sterowany):** Sygnał na wyjściu układu, który jest wynikiem działania sygnału wejściowego. Oznaczany jako `y(t)` lub `x(t)`.
*   **Sygnał zakłócający:** Niepożądany sygnał, który wpływa na działanie układu i może pogorszyć jakość sterowania. Oznaczany jako `z(t)`.

**Klasyfikacja układów:**

*   **Liniowe i nieliniowe:** Układy liniowe spełniają zasadę superpozycji, co oznacza, że odpowiedź na sumę sygnałów wejściowych jest równa sumie odpowiedzi na poszczególne sygnały. Układy nieliniowe tej zasady nie spełniają.
*   **Statyczne i astatyczne:** Układy statyczne po ustaniu wymuszenia wracają do stanu równowagi. Układy astatyczne nie mają tej właściwości i po ustaniu wymuszenia mogą pozostawać w nowym stanie.

### 2. Transformacja Laplace'a

Transformacja Laplace'a jest narzędziem matematycznym, które pozwala na zamianę równań różniczkowych zwyczajnych na równania algebraiczne. Jest to niezwykle przydatne w analizie układów dynamicznych.

**Definicja:**

Transformatą Laplace'a funkcji `f(t)` nazywamy funkcję `F(s)` zdefiniowaną wzorem:

$$ F(s) = \mathcal{L}\{f(t)\} = \int_{0}^{\infty} f(t)e^{-st} dt $$

**Transformata odwrotna:**

Operację odwrotną do transformacji Laplace'a nazywamy transformatą odwrotną i oznaczamy jako `f(t) = L^-1{F(s)}`.

**ZADANIE 1: Obliczanie transformaty prostych funkcji**

Oblicz transformatę Laplace'a dla funkcji `f(t) = 1` (skok jednostkowy).

**Rozwiązanie:**

$$ F(s) = \int_{0}^{\infty} 1 \cdot e^{-st} dt = [-\frac{1}{s}e^{-st}]_{0}^{\infty} = -\frac{1}{s}(0 - 1) = \frac{1}{s} $$

### 3. Funkcja transmitancji

Funkcja transmitancji (transmitancja operatorowa) jest podstawowym modelem matematycznym układu liniowego. Definiuje się ją jako stosunek transformaty Laplace'a sygnału wyjściowego `Y(s)` do transformaty Laplace'a sygnału wejściowego `U(s)`, przy zerowych warunkach początkowych.

$$ G(s) = \frac{Y(s)}{U(s)} $$

**ZADANIE 2: Wyznaczanie transmitancji z równania różniczkowego**

Wyznacz transmitancję dla obiektu opisanego równaniem różniczkowym: `y''(t) + 3y'(t) + 2y(t) = 4u(t)`.

**Rozwiązanie:**

Stosujemy transformatę Laplace'a do obu stron równania, pamiętając o własnościach dotyczących pochodnych:

$$ s^2Y(s) + 3sY(s) + 2Y(s) = 4U(s) $$
$$ Y(s)(s^2 + 3s + 2) = 4U(s) $$
$$ G(s) = \frac{Y(s)}{U(s)} = \frac{4}{s^2 + 3s + 2} $$

### 4. Algebra schematów blokowych

Schematy blokowe są graficzną reprezentacją układów sterowania. Umożliwiają one łatwiejszą analizę i syntezę złożonych systemów. Podstawowe operacje na schematach blokowych to:

*   **Połączenie szeregowe:** Dwa lub więcej elementów połączonych jeden za drugim. Transmitancja zastępcza jest iloczynem transmitancji poszczególnych elementów.

    $$ G(s) = G_1(s) \cdot G_2(s) $$

*   **Połączenie równoległe:** Dwa lub więcej elementów połączonych wejściami i wyjściami. Transmitancja zastępcza jest sumą transmitancji poszczególnych elementów.

    $$ G(s) = G_1(s) + G_2(s) $$

*   **Sprzężenie zwrotne:** Sygnał wyjściowy jest podawany z powrotem na wejście, tworząc pętlę. Jest to najczęściej spotykany rodzaj połączenia w układach regulacji.

    $$ G(s) = \frac{G_1(s)}{1 \pm G_1(s)G_2(s)} $$

    Znak w mianowniku zależy od rodzaju sprzężenia (ujemne lub dodatnie).

**ZADANIE 3: Upraszczanie schematu blokowego**

Uprość schemat blokowy składający się z dwóch bloków w pętli sprzężenia zwrotnego: `G1(s) = 2/(s+1)` i `G2(s) = 1/s`.

**Rozwiązanie:**

Stosujemy wzór na sprzężenie zwrotne ujemne:

$$ G(s) = \frac{G_1(s)}{1 + G_1(s)G_2(s)} = \frac{\frac{2}{s+1}}{1 + \frac{2}{s+1} \cdot \frac{1}{s}} = \frac{\frac{2}{s+1}}{\frac{s(s+1) + 2}{s(s+1)}} = \frac{2s}{s^2 + s + 2} $$

### 5. Charakterystyki dynamiczne

Charakterystyki dynamiczne opisują zachowanie się układu w czasie po podaniu na wejście określonego sygnału. Najważniejsze z nich to:

*   **Odpowiedź skokowa:** Odpowiedź układu na sygnał wejściowy w postaci skoku jednostkowego (`u(t) = 1`, `U(s) = 1/s`).

    $$ y_{skok}(t) = \mathcal{L}^{-1}\{G(s) \cdot \frac{1}{s}\} $$

*   **Odpowiedź impulsowa:** Odpowiedź układu na sygnał wejściowy w postaci impulsu Diraca (`u(t) = δ(t)`, `U(s) = 1`).

    $$ y_{imp}(t) = \mathcal{L}^{-1}\{G(s)\} $$

**ZADANIE 4: Wyznaczanie odpowiedzi skokowej**

Wyznacz odpowiedź skokową dla obiektu o transmitancji `G(s) = 1/(s+a)`.

**Rozwiązanie:**

$$ Y(s) = G(s) \cdot \frac{1}{s} = \frac{1}{s(s+a)} $$

Rozkładamy na ułamki proste:

$$ \frac{1}{s(s+a)} = \frac{A}{s} + \frac{B}{s+a} $$
$$ A = \lim_{s \to 0} s \cdot \frac{1}{s(s+a)} = \frac{1}{a} $$
$$ B = \lim_{s \to -a} (s+a) \cdot \frac{1}{s(s+a)} = -\frac{1}{a} $$

Zatem:

$$ Y(s) = \frac{1}{a} \cdot \frac{1}{s} - \frac{1}{a} \cdot \frac{1}{s+a} $$

Stosując odwrotną transformatę Laplace'a otrzymujemy:

$$ y(t) = \frac{1}{a}(1 - e^{-at}) $$

## CZĘŚĆ II: STABILNOŚĆ UKŁADÓW

### 6. Pojęcie stabilności

Stabilność jest jedną z najważniejszych właściwości układów dynamicznych. Układ jest stabilny, jeśli jego odpowiedź na ograniczone pobudzenie jest również ograniczona. Innymi słowy, stabilny układ nie "wybucha" i jego sygnał wyjściowy dąży do pewnej ustalonej wartości lub pozostaje w ograniczonym zakresie.

**Warunki stabilności:**

Warunkiem koniecznym i wystarczającym stabilności układu liniowego jest, aby wszystkie pierwiastki równania charakterystycznego (mianownika transmitancji) miały ujemne części rzeczywiste. Oznacza to, że wszystkie bieguny transmitancji muszą leżeć w lewej półpłaszczyźnie zespolonej.

### 7. Kryterium stabilności Hurwitza

Kryterium Hurwitza jest algebraiczną metodą badania stabilności układów liniowych. Pozwala ono na określenie, czy wszystkie pierwiastki wielomianu charakterystycznego mają ujemne części rzeczywiste, bez konieczności ich obliczania.

**Procedura:**

1.  Zapisz wielomian charakterystyczny układu: `M(s) = a_n s^n + a_{n-1} s^{n-1} + ... + a_1 s + a_0`.
2.  Utwórz macierz Hurwitza `H` o wymiarach `n x n`:

    $$ H = \begin{pmatrix}
a_{n-1} & a_{n-3} & a_{n-5} & \dots \\
a_n & a_{n-2} & a_{n-4} & \dots \\
0 & a_{n-1} & a_{n-3} & \dots \\
\vdots & \vdots & \vdots & \ddots
\end{pmatrix} $$

3.  Oblicz kolejne podwyznaczniki główne (minory) macierzy Hurwitza: `Δ_1, Δ_2, ..., Δ_n`.

**Warunek stabilności:**

Układ jest stabilny, jeśli wszystkie współczynniki wielomianu charakterystycznego `a_i` są dodatnie oraz wszystkie podwyznaczniki główne macierzy Hurwitza `Δ_i` są dodatnie.

**ZADANIE 5: Badanie stabilności metodą Hurwitza**

Zbadać stabilność układu o wielomianie charakterystycznym: `s^4 + 2s^3 + 6s^2 - 2s + 8`.

**Rozwiązanie:**

Warunek konieczny stabilności nie jest spełniony, ponieważ jeden ze współczynników (`-2`) jest ujemny. Układ jest **niestabilny**.

**ZADANIE 6: Wyznaczanie obszaru stabilności**

Wyznacz obszar stabilności dla układu o wielomianie charakterystycznym: `s^3 + 3s^2 + (k+2)s + 2`.

**Rozwiązanie:**

Wielomian charakterystyczny: `M(s) = s^3 + 3s^2 + (k+2)s + 2`.

Współczynniki: `a_3=1, a_2=3, a_1=k+2, a_0=2`.

Warunki konieczne:
1.  `a_3 > 0` (spełniony)
2.  `a_2 > 0` (spełniony)
3.  `a_1 > 0` => `k+2 > 0` => `k > -2`
4.  `a_0 > 0` (spełniony)

Macierz Hurwitza:

$$ H = \begin{pmatrix}
3 & 2 \\
1 & k+2
\end{pmatrix} $$

Podwyznaczniki:
`Δ_1 = 3 > 0`
`Δ_2 = 3(k+2) - 2 = 3k + 6 - 2 = 3k + 4 > 0` => `3k > -4` => `k > -4/3`

Ostatecznie, aby układ był stabilny, `k` musi spełniać oba warunki: `k > -2` i `k > -4/3`. Zatem obszar stabilności to `k > -4/3`.

## CZĘŚĆ III: REGULATORY I UKŁADY REGULACJI

### 8. Rodzaje regulatorów

Regulatory są kluczowymi elementami układów automatycznej regulacji. Ich zadaniem jest takie modyfikowanie sygnału sterującego, aby uchyb regulacji (różnica między wartością zadaną a wartością mierzoną) był jak najmniejszy.

*   **Regulator proporcjonalny (P):** Sygnał na wyjściu regulatora jest proporcjonalny do uchybu regulacji. Charakteryzuje się szybką reakcją, ale zazwyczaj pozostawia uchyb ustalony.

    $$ G_R(s) = K_p $$

*   **Regulator całkujący (I):** Sygnał na wyjściu regulatora jest proporcjonalny do całki uchybu. Eliminuje uchyb ustalony, ale może spowolnić odpowiedź układu i wprowadzić oscylacje.

    $$ G_R(s) = \frac{K_i}{s} $$

*   **Regulator różniczkujący (D):** Sygnał na wyjściu regulatora jest proporcjonalny do pochodnej uchybu. Przyspiesza reakcję układu i tłumi oscylacje, ale jest wrażliwy na szumy pomiarowe.

    $$ G_R(s) = K_d s $$

*   **Regulatory złożone:**
    *   **PI:** Połączenie regulatora proporcjonalnego i całkującego. Łączy zalety obu: szybką reakcję i eliminację uchybu ustalonego.

        $$ G_R(s) = K_p (1 + \frac{1}{T_i s}) $$

    *   **PD:** Połączenie regulatora proporcjonalnego i różniczkującego. Poprawia stabilność i szybkość odpowiedzi.

        $$ G_R(s) = K_p (1 + T_d s) $$

    *   **PID:** Połączenie wszystkich trzech członów. Zapewnia najlepszą jakość regulacji, ale wymaga strojenia trzech parametrów.

        $$ G_R(s) = K_p (1 + \frac{1}{T_i s} + T_d s) $$

### 9. Transmitancja operatorowa układu regulacji

Analiza układu regulacji polega na wyznaczeniu jego transmitancji zastępczej, która opisuje zależność między wartością zadaną a wartością wyjściową. Schemat typowego układu regulacji jednopętlowej przedstawiono poniżej.

**ZADANIE 7: Analiza układu z regulatorem**

Wyznacz transmitancję zastępczą dla układu z regulatorem `GR(s)` i obiektem `Gs(s)` w pętli sprzężenia zwrotnego.

**Rozwiązanie:**

Transmitancja układu otwartego wynosi `G_o(s) = G_R(s)G_s(s)`. Transmitancja układu zamkniętego (zastępcza) wynosi:

$$ G(s) = \frac{G_o(s)}{1 + G_o(s)} = \frac{G_R(s)G_s(s)}{1 + G_R(s)G_s(s)} $$

### 10. Model w przestrzeni stanu

Model w przestrzeni stanu jest alternatywną metodą opisu układów dynamicznych, szczególnie przydatną dla układów wielowymiarowych i nieliniowych. Układ jest opisywany przez zestaw równań stanu i równanie wyjścia w postaci macierzowej:

$$ \dot{\mathbf{x}}(t) = \mathbf{A}\mathbf{x}(t) + \mathbf{B}\mathbf{u}(t) $$
$$ \mathbf{y}(t) = \mathbf{C}\mathbf{x}(t) + \mathbf{D}\mathbf{u}(t) $$

*   `x(t)` - wektor stanu
*   `u(t)` - wektor wejść (sterowań)
*   `y(t)` - wektor wyjść
*   `A` - macierz stanu
*   `B` - macierz wejść
*   `C` - macierz wyjść
*   `D` - macierz przenoszenia

**ZADANIE 8: Wyznaczanie transmitancji operatorowej z modelu w przestrzeni stanu**

Wyznacz transmitancję operatorową dla układu opisanego macierzami:
`A = [[-3, 1, 5], [-1, -2, 0], [1, 0, 0]]`, `B = [[2], [0], [3]]`, `C = [0, 2, 3]`, `D = [3]`

**Rozwiązanie:**

Transmitancję operatorową z modelu w przestrzeni stanu oblicza się ze wzoru:

$$ G(s) = \mathbf{C}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B} + \mathbf{D} $$

Obliczenia są dość złożone i wymagają odwrócenia macierzy `(sI - A)`. Dla tego przykładu, po wykonaniu obliczeń, otrzymalibyśmy transmitancję w postaci ułamka wymiernego.

## CZĘŚĆ IV: ZADANIA KOMPLEKSOWE

### 11. Uchyb regulacji w stanie ustalonym

Uchyb regulacji w stanie ustalonym (`e_ss`) to różnica między wartością zadaną a wartością sygnału wyjściowego po ustabilizowaniu się układu (gdy `t -> ∞`). Jest to ważny wskaźnik jakości regulacji.

Uchyb ustalony można obliczyć za pomocą twierdzenia o wartości końcowej:

$$ e_{ss} = \lim_{t \to \infty} e(t) = \lim_{s \to 0} sE(s) $$

Gdzie `E(s)` to transformata Laplace'a sygnału uchybu `e(t) = x_zad(t) - x(t)`.

**ZADANIE 9: Wyznaczanie uchybu regulacji w stanie ustalonym**

Rozważmy układ z obrazka `Drugi2(1).JPG`. Wyznacz uchyb regulacji w stanie ustalonym dla różnych typów regulatorów `GR(s)`.

Dane:
*   `Gs(s) = 1 / ((sT1+1)(sT2+1)sT3)`
*   `Z(s) = 1/s` (zakłócenie)
*   `X_zad(s) = 1/s` (wartość zadana)

**Rozwiązanie:**

Sygnał uchybu `E(s)` w tym układzie jest równy `X_zad(s) - X(s)`. Na podstawie schematu blokowego możemy wyprowadzić wzór na `X(s)`:

$$ X(s) = ( (X_{zad}(s) - X(s))G_R(s) + Z(s) ) G_S(s) $$
$$ X(s)(1 + G_R(s)G_S(s)) = X_{zad}(s)G_R(s)G_S(s) + Z(s)G_S(s) $$
$$ X(s) = \frac{X_{zad}(s)G_R(s)G_S(s) + Z(s)G_S(s)}{1 + G_R(s)G_S(s)} $$

Uchyb `E(s) = X_{zad}(s) - X(s)`:

$$ E(s) = X_{zad}(s) - \frac{X_{zad}(s)G_R(s)G_S(s) + Z(s)G_S(s)}{1 + G_R(s)G_S(s)} = \frac{X_{zad}(s)(1 + G_R(s)G_S(s)) - X_{zad}(s)G_R(s)G_S(s) - Z(s)G_S(s)}{1 + G_R(s)G_S(s)} $$
$$ E(s) = \frac{X_{zad}(s) - Z(s)G_S(s)}{1 + G_R(s)G_S(s)} $$

Podstawiając `X_zad(s) = 1/s` i `Z(s) = 1/s`:

$$ E(s) = \frac{1/s - (1/s)G_S(s)}{1 + G_R(s)G_S(s)} = \frac{1-G_S(s)}{s(1 + G_R(s)G_S(s))} $$

Teraz możemy obliczyć uchyb ustalony `e_ss`:

$$ e_{ss} = \lim_{s \to 0} sE(s) = \lim_{s \to 0} \frac{1-G_S(s)}{1 + G_R(s)G_S(s)} $$

Ponieważ `lim_{s->0} Gs(s) = ∞` (ze względu na człon `1/s` w `Gs(s)`), to wyrażenie `1 - Gs(s)` również dąży do nieskończoności. Aby obliczyć granicę, musimy przeanalizować rząd astatyzmu.

Analiza dla **regulatora P** (`GR(s) = Kp`):
Układ otwarty `Go(s) = Kp * Gs(s)` ma rząd astatyzmu 1. Uchyb ustalony od wymuszenia `X_zad` będzie zerowy, ale od zakłócenia `Z` będzie stały i różny od zera.

Analiza dla **regulatora PI** (`GR(s) = Kp(1 + 1/(Ti*s))`):
Układ otwarty `Go(s)` będzie miał rząd astatyzmu 2. Uchyb ustalony od wymuszenia `X_zad` i zakłócenia `Z` będzie zerowy.

## DODATKI

### A. Tablice transformat Laplace'a

| f(t) | F(s) |
|---|---|
| 1(t) | 1/s |
| t | 1/s^2 |
| e^{-at} | 1/(s+a) |
| sin(ωt) | ω/(s^2 + ω^2) |
| cos(ωt) | s/(s^2 + ω^2) |

### B. Słowniczek pojęć

*   **Astatyzm:** Właściwość układu sterowania, która określa jego zdolność do eliminacji uchybu ustalonego dla określonych typów sygnałów wejściowych.
*   **Bieguny transmitancji:** Pierwiastki mianownika funkcji transmitancji. Ich położenie na płaszczyźnie zespolonej decyduje o stabilności układu.
*   **Równanie charakterystyczne:** Mianownik transmitancji układu zamkniętego przyrównany do zera.
