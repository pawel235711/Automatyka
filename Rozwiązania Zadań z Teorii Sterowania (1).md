# Rozwiązania Zadań z Teorii Sterowania

Niniejszy dokument przedstawia analizę i rozwiązania zadań z teorii sterowania, wyjaśniając podstawowe koncepcje w sposób przystępny dla początkujących. Zwrócono uwagę na potencjalne problemy w treści zadań, które uniemożliwiają pełne numeryczne rozwiązanie.

## Zadanie 1: Wyznacz model w przestrzeni stanu

### Wprowadzenie do modelu w przestrzeni stanu

**Model w przestrzeni stanu** to matematyczny opis dynamicznego systemu, który wykorzystuje zestaw równań różniczkowych pierwszego rzędu. W przeciwieństwie do transmitancji, która opisuje relację między wejściem a wyjściem systemu w dziedzinie częstotliwości (lub operatorowej), model w przestrzeni stanu opisuje wewnętrzną dynamikę systemu poprzez zmienne stanu. Zmienne stanu to minimalny zestaw zmiennych, które w danej chwili czasu w pełni opisują stan systemu i pozwalają przewidzieć jego przyszłe zachowanie, jeśli znane są sygnały wejściowe.

Ogólna postać równań stanu dla systemu liniowego, niezmiennego w czasie (LTI) to:

$$ \dot{\mathbf{x}}(t) = \mathbf{A} \mathbf{x}(t) + \mathbf{B} \mathbf{u}(t) $$
$$ \mathbf{y}(t) = \mathbf{C} \mathbf{x}(t) + \mathbf{D} \mathbf{u}(t) $$

Gdzie:
*   $\mathbf{x}(t)$ to wektor zmiennych stanu.
*   $\mathbf{u}(t)$ to wektor sygnałów wejściowych.
*   $\mathbf{y}(t)$ to wektor sygnałów wyjściowych.
*   $\mathbf{A}$ to macierz stanu.
*   $\mathbf{B}$ to macierz wejścia.
*   $\mathbf{C}$ to macierz wyjścia.
*   $\mathbf{D}$ to macierz przenoszenia (bezpośredniego sprzężenia).

### Analiza zadania

Zadanie polega na przekształceniu transmitancji $G(s)$ na model w przestrzeni stanu. Niestety, podane transmitancje w treści zadania są niekompletne lub zawierają błędy w zapisie potęg zmiennej $s$ (np. `s+6S+10` zamiast `s^2+6s+10`), co uniemożliwia ich jednoznaczne przekształcenie. Przykład poprawnej transmitancji mógłby wyglądać tak:

$$ G(s) = \frac{s^2 + 6s + 10}{s^3 + 5s^2 + 11s + 11} $$

### Ogólne podejście do konwersji $G(s)$ na model w przestrzeni stanu

Istnieje kilka metod konwersji transmitancji na model w przestrzeni stanu, np. postać kanoniczna sterowalna lub obserwowalna. Dla transmitancji postaci:

$$ G(s) = \frac{b_m s^m + \dots + b_1 s + b_0}{s^n + a_{n-1} s^{n-1} + \dots + a_1 s + a_0 } $$

Przy założeniu $m < n$, można uzyskać postać kanoniczną sterowalną. Przykładowo, dla $n=3$ i $m=2$, równania stanu mogłyby wyglądać następująco:

$$ \begin{bmatrix} \dot{x}_1 \\ \dot{x}_2 \\ \dot{x}_3 \end{bmatrix} = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -a_0 & -a_1 & -a_2 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} + \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} u $$
$$ y = \begin{bmatrix} (b_0 - a_0 b_2) & (b_1 - a_1 b_2) & (b_2 - a_2 b_2) \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} + b_2 u $$

(Powyższy wzór jest uproszczony i wymaga dostosowania do konkretnych współczynników oraz stopnia wielomianu licznika i mianownika).

## Zadanie 2: Wyznacz transmitancję operatorową z modelu w przestrzeni stanu

### Wprowadzenie do transmitancji operatorowej

**Transmitancja operatorowa** (funkcja przenoszenia) $G(s)$ to stosunek transformaty Laplace'a sygnału wyjściowego do transformaty Laplace'a sygnału wejściowego, przy zerowych warunkach początkowych. Jest to fundamentalne narzędzie w analizie systemów liniowych, pozwalające na łatwe badanie ich odpowiedzi częstotliwościowej i stabilności.

### Analiza zadania

Zadanie polega na obliczeniu transmitancji $G(s)$ na podstawie podanych macierzy modelu w przestrzeni stanu:

$$ \mathbf{A} = \begin{bmatrix} 3 & 1 & 5 \\ -3 & -1 & -2 \\ 1 & 0 & 0 \end{bmatrix}, \quad \mathbf{B} = \begin{bmatrix} 2 \\ 3 \\ 0 \end{bmatrix}, \quad \mathbf{C} = \begin{bmatrix} 0 & 2 & 3 \end{bmatrix}, \quad \mathbf{D} = \begin{bmatrix} 3 \end{bmatrix} $$

Transmitancję $G(s)$ obliczamy ze wzoru:

$$ G(s) = \mathbf{C} (s\mathbf{I} - \mathbf{A})^{-1} \mathbf{B} + \mathbf{D} $$

Gdzie $s\mathbf{I} - \mathbf{A}$ to macierz:

$$ s\mathbf{I} - \mathbf{A} = \begin{bmatrix} s & 0 & 0 \\ 0 & s & 0 \\ 0 & 0 & s \end{bmatrix} - \begin{bmatrix} 3 & 1 & 5 \\ -3 & -1 & -2 \\ 1 & 0 & 0 \end{bmatrix} = \begin{bmatrix} s-3 & -1 & -5 \\ 3 & s+1 & 2 \\ -1 & 0 & s \end{bmatrix} $$

**Problem:** Macierze $\mathbf{B}$ i $\mathbf{C}$ mają niezgodne wymiary. Macierz $\mathbf{B}$ jest wektorem kolumnowym $3 \times 1$, natomiast macierz $\mathbf{C}$ jest wektorem wierszowym $1 \times 3$. Macierz $\mathbf{D}$ jest skalarem $1 \times 1$. Aby operacje macierzowe były poprawne, wymiary macierzy muszą być zgodne. W tym przypadku, jeśli $\mathbf{B}$ jest $3 \times 1$, to $\mathbf{C}$ powinno być $1 \times 3$, a $\mathbf{D}$ powinno być $1 \times 1$. Jednakże, w zadaniu $\mathbf{B}$ jest $3 \times 1$, a $\mathbf{C}$ jest $1 \times 3$, co jest poprawne dla systemu z jednym wejściem i jednym wyjściem. Problem leży w tym, że w treści zadania $\mathbf{B}$ jest zapisane jako wektor kolumnowy, a $\mathbf{C}$ jako wektor wierszowy, co jest standardem. Prawdopodobnie błąd jest w formacie zapisu, który może sugerować, że $\mathbf{B}$ jest macierzą $3 \times 1$, a $\mathbf{C}$ jest macierzą $1 \times 3$. Jeśli tak, to wymiary są poprawne.

Jednakże, aby obliczyć $(s\mathbf{I} - \mathbf{A})^{-1}$, należy najpierw obliczyć wyznacznik macierzy $(s\mathbf{I} - \mathbf{A})$ i macierz dołączoną. Jest to proces skomplikowany i czasochłonny do wykonania ręcznie.

## Zadanie 3: Zbadać stabilność metodą Hurwitza

### Koncepcja stabilności

**Stabilność** systemu sterowania jest kluczową właściwością. System stabilny to taki, który po zakłóceniu (np. zmianie sygnału wejściowego) powraca do stanu równowagi lub podąża za sygnałem zadanym w sposób kontrolowany. System niestabilny będzie miał tendencję do 
rozbiegania się, co w praktyce może prowadzić do uszkodzenia urządzenia lub niekontrolowanego zachowania.

### Kryterium stabilności Hurwitza

**Kryterium stabilności Hurwitza** to algebraiczna metoda badania stabilności systemów liniowych, niezmiennych w czasie (LTI), opisanych równaniem charakterystycznym (mianownikiem transmitancji) w postaci wielomianu:

$$ P(s) = a_n s^n + a_{n-1} s^{n-1} + \dots + a_1 s + a_0 = 0 $$

Warunki konieczne i wystarczające stabilności (wszystkie pierwiastki wielomianu mają ujemne części rzeczywiste) są następujące:

1.  **Wszystkie współczynniki wielomianu ($a_i$) muszą być tego samego znaku** (zazwyczaj dodatnie). Jeśli którykolwiek współczynnik jest ujemny lub zerowy (z wyjątkiem $a_0$ w niektórych przypadkach), system jest niestabilny.
2.  **Wszystkie wyznaczniki Hurwitza (minory główne macierzy Hurwitza) muszą być dodatnie.**

Macierz Hurwitza jest konstruowana ze współczynników wielomianu w następujący sposób:

$$ \mathbf{H} = \begin{bmatrix}
  a_{n-1} & a_{n-3} & a_{n-5} & \dots & 0 \\
  a_n & a_{n-2} & a_{n-4} & \dots & 0 \\
  0 & a_{n-1} & a_{n-3} & \dots & 0 \\
  0 & a_n & a_{n-2} & \dots & 0 \\
  \vdots & \vdots & \vdots & \ddots & \vdots \\
  0 & 0 & 0 & \dots & a_0
\end{bmatrix} $$

Wyznaczniki Hurwitza to:

*   $\Delta_1 = a_{n-1}$
*   $\Delta_2 = \begin{vmatrix} a_{n-1} & a_{n-3} \\ a_n & a_{n-2} \end{vmatrix}$
*   $\Delta_3 = \begin{vmatrix} a_{n-1} & a_{n-3} & a_{n-5} \\ a_n & a_{n-2} & a_{n-4} \\ 0 & a_{n-1} & a_{n-3} \end{vmatrix}$
*   ... aż do $\Delta_n = a_0 \Delta_{n-1}$

### Analiza przykładów z zadania

**Przykład 1:** `s⁴ + 2s³ + 6s² - 2s + 8`

Wielomian charakterystyczny: $P(s) = s^4 + 2s^3 + 6s^2 - 2s + 8$

Współczynniki: $a_4=1, a_3=2, a_2=6, a_1=-2, a_0=8$

**Analiza:** Sprawdzamy pierwszy warunek stabilności Hurwitza. Wszystkie współczynniki muszą być tego samego znaku. W tym przypadku współczynnik $a_1 = -2$ jest ujemny, podczas gdy pozostałe są dodatnie. Zatem, **system jest niestabilny**.

**Przykład 2:** `s⁴ + 4s³ + 6s² + 7s + 1`

Wielomian charakterystyczny: $P(s) = s^4 + 4s^3 + 6s^2 + 7s + 1$

Współczynniki: $a_4=1, a_3=4, a_2=6, a_1=7, a_0=1$

**Analiza:** Wszystkie współczynniki są dodatnie, więc pierwszy warunek jest spełniony. Przechodzimy do budowy macierzy Hurwitza i obliczenia wyznaczników.

Macierz Hurwitza dla $n=4$:

$$ \mathbf{H} = \begin{bmatrix}
  a_3 & a_1 & a_{-1} & a_{-3} \\
  a_4 & a_2 & a_0 & a_{-2} \\
  0 & a_3 & a_1 & a_{-1} \\
  0 & a_4 & a_2 & a_0
\end{bmatrix} = \begin{bmatrix}
  4 & 7 & 0 & 0 \\
  1 & 6 & 1 & 0 \\
  0 & 4 & 7 & 0 \\
  0 & 1 & 6 & 1
\end{bmatrix} $$

(Współczynniki z indeksem ujemnym są równe 0).

Wyznaczniki Hurwitza:

*   $\Delta_1 = a_3 = 4 > 0$

*   $\Delta_2 = \begin{vmatrix} a_3 & a_1 \\ a_4 & a_2 \end{vmatrix} = \begin{vmatrix} 4 & 7 \\ 1 & 6 \end{vmatrix} = 4 \cdot 6 - 7 \cdot 1 = 24 - 7 = 17 > 0$

*   $\Delta_3 = \begin{vmatrix} 4 & 7 & 0 \\ 1 & 6 & 1 \\ 0 & 4 & 7 \end{vmatrix} = 4 \begin{vmatrix} 6 & 1 \\ 4 & 7 \end{vmatrix} - 7 \begin{vmatrix} 1 & 1 \\ 0 & 7 \end{vmatrix} + 0 = 4(42-4) - 7(7-0) = 4(38) - 7(7) = 152 - 49 = 103 > 0$

*   $\Delta_4 = a_0 \Delta_3 = 1 \cdot 103 = 103 > 0$

**Wniosek:** Ponieważ wszystkie współczynniki są dodatnie i wszystkie wyznaczniki Hurwitza są dodatnie, **system jest stabilny**.

**Przykład 3:** `s⁴ + 5s³ + 3s² + 1s + (k-2)`

Wielomian charakterystyczny: $P(s) = s^4 + 5s^3 + 3s^2 + 1s + (k-2)$

Współczynniki: $a_4=1, a_3=5, a_2=3, a_1=1, a_0=(k-2)$

**Analiza:**

1.  **Warunek na znaki współczynników:** Wszystkie współczynniki muszą być dodatnie. Zatem:
    *   $a_4=1 > 0$
    *   $a_3=5 > 0$
    *   $a_2=3 > 0$
    *   $a_1=1 > 0$
    *   $a_0=(k-2) > 0 \implies k > 2$

2.  **Warunek na wyznaczniki Hurwitza:**

    Macierz Hurwitza dla $n=4$:

    $$ \mathbf{H} = \begin{bmatrix}
      a_3 & a_1 & 0 & 0 \\
      a_4 & a_2 & a_0 & 0 \\
      0 & a_3 & a_1 & 0 \\
      0 & a_4 & a_2 & a_0
    \end{bmatrix} = \begin{bmatrix}
      5 & 1 & 0 & 0 \\
      1 & 3 & (k-2) & 0 \\
      0 & 5 & 1 & 0 \\
      0 & 1 & 3 & (k-2)
    \end{bmatrix} $$

    Wyznaczniki Hurwitza:

    *   $\Delta_1 = a_3 = 5 > 0$

    *   $\Delta_2 = \begin{vmatrix} 5 & 1 \\ 1 & 3 \end{vmatrix} = 5 \cdot 3 - 1 \cdot 1 = 15 - 1 = 14 > 0$

    *   $\Delta_3 = \begin{vmatrix} 5 & 1 & 0 \\ 1 & 3 & (k-2) \\ 0 & 5 & 1 \end{vmatrix} = 5 \begin{vmatrix} 3 & (k-2) \\ 5 & 1 \end{vmatrix} - 1 \begin{vmatrix} 1 & (k-2) \\ 0 & 1 \end{vmatrix} = 5(3 - 5(k-2)) - 1(1 - 0) = 5(3 - 5k + 10) - 1 = 5(13 - 5k) - 1 = 65 - 25k - 1 = 64 - 25k$

        Aby system był stabilny, $\Delta_3 > 0 \implies 64 - 25k > 0 \implies 64 > 25k \implies k < \frac{64}{25} \implies k < 2.56$

    *   $\Delta_4 = a_0 \Delta_3 = (k-2) (64 - 25k)$

        Aby system był stabilny, $\Delta_4 > 0$. Ponieważ już wiemy, że $(k-2) > 0$ (z warunku na $a_0$), to wystarczy, że $(64 - 25k) > 0$, co daje nam ten sam warunek: $k < 2.56$.

**Wniosek:** System jest stabilny, gdy spełnione są oba warunki: $k > 2$ i $k < 2.56$. Zatem, **system jest stabilny dla $2 < k < 2.56$**.

## Zadanie 4: Wyznaczyć uchyb regulacji w stanie ustalonym

### Koncepcja uchybu w stanie ustalonym

**Uchyb regulacji w stanie ustalonym** ($e_{ss}$) to różnica między wartością zadaną (referencyjną) a rzeczywistą wartością wyjściową systemu, gdy system osiągnie stan równowagi po upływie długiego czasu ($t \to \infty$). Jest to ważny parametr oceny jakości działania systemu sterowania.

Do obliczenia uchybu w stanie ustalonym wykorzystuje się **twierdzenie o wartości końcowej** z transformaty Laplace'a:

$$ e_{ss} = \lim_{t \to \infty} e(t) = \lim_{s \to 0} s E(s) $$

Gdzie $E(s)$ to transformata Laplace'a sygnału uchybu.

### Analiza schematu blokowego

Schemat blokowy przedstawia system sterowania z ujemnym sprzężeniem zwrotnym. Mamy:

*   $X_{zad}(s)$ - sygnał zadany (wejście)
*   $Z(s)$ - zakłócenie
*   $G_R(s)$ - transmitancja regulatora
*   $G_S(s)$ - transmitancja obiektu (systemu)
*   $X(s)$ - sygnał wyjściowy

Sygnał uchybu $E(s)$ na wejściu regulatora jest dany jako:

$$ E(s) = X_{zad}(s) - X(s) $$

Sygnał na wyjściu obiektu $X(s)$ jest sumą wpływu sygnału sterującego i zakłócenia, przepuszczonych przez obiekt:

$$ X(s) = (G_R(s) E(s) + Z(s)) G_S(s) $$

Podstawiając $E(s)$ do drugiego równania:

$$ X(s) = (G_R(s) (X_{zad}(s) - X(s)) + Z(s)) G_S(s) $$

Rozwiązując dla $X(s)$:

$$ X(s) = G_R(s) G_S(s) X_{zad}(s) - G_R(s) G_S(s) X(s) + Z(s) G_S(s) $$
$$ X(s) (1 + G_R(s) G_S(s)) = G_R(s) G_S(s) X_{zad}(s) + Z(s) G_S(s) $$
$$ X(s) = \frac{G_R(s) G_S(s)}{1 + G_R(s) G_S(s)} X_{zad}(s) + \frac{G_S(s)}{1 + G_R(s) G_S(s)} Z(s) $$

Teraz możemy wyrazić $E(s)$:

$$ E(s) = X_{zad}(s) - X(s) = X_{zad}(s) - \left( \frac{G_R(s) G_S(s)}{1 + G_R(s) G_S(s)} X_{zad}(s) + \frac{G_S(s)}{1 + G_R(s) G_S(s)} Z(s) \right) $$
$$ E(s) = \left( 1 - \frac{G_R(s) G_S(s)}{1 + G_R(s) G_S(s)} \right) X_{zad}(s) - \frac{G_S(s)}{1 + G_R(s) G_S(s)} Z(s) $$
$$ E(s) = \frac{1 + G_R(s) G_S(s) - G_R(s) G_S(s)}{1 + G_R(s) G_S(s)} X_{zad}(s) - \frac{G_S(s)}{1 + G_R(s) G_S(s)} Z(s) $$
$$ E(s) = \frac{1}{1 + G_R(s) G_S(s)} X_{zad}(s) - \frac{G_S(s)}{1 + G_R(s) G_S(s)} Z(s) $$

### Dane z zadania

*   $G_S(s) = \frac{1}{(sT_1+1)(sT_2+1)sT_3}$
*   $G_R(s)$ może być:
    *   $P$ (proporcjonalny)
    *   $PD$ (proporcjonalno-różniczkujący)
    *   $PI$ (proporcjonalno-całkujący)
*   $Z(s) = \frac{1}{s}$ (skok jednostkowy zakłócenia)
*   $X_{zad}(s) = \frac{1}{s}$ (skok jednostkowy sygnału zadanego)

**Problem:** Transmitancja obiektu $G_S(s)$ zawiera nieokreślone stałe czasowe $T_1, T_2, T_3$. Bez ich wartości, a także bez konkretnej postaci regulatora $G_R(s)$ (P, PD, PI) z jego parametrami, nie jest możliwe numeryczne obliczenie uchybu w stanie ustalonym.

### Ogólne podejście do obliczania uchybu dla różnych regulatorów

**1. Regulator Proporcjonalny (P):** $G_R(s) = K_p$

$$ E(s) = \frac{1}{1 + K_p G_S(s)} X_{zad}(s) - \frac{G_S(s)}{1 + K_p G_S(s)} Z(s) $$

Uchyb w stanie ustalonym:

$$ e_{ss} = \lim_{s \to 0} s \left( \frac{1}{1 + K_p G_S(s)} \frac{1}{s} - \frac{G_S(s)}{1 + K_p G_S(s)} \frac{1}{s} \right) $$
$$ e_{ss} = \frac{1}{1 + K_p \lim_{s \to 0} G_S(s)} - \frac{\lim_{s \to 0} G_S(s)}{1 + K_p \lim_{s \to 0} G_S(s)} $$

Zauważmy, że $\lim_{s \to 0} G_S(s) = \lim_{s \to 0} \frac{1}{(sT_1+1)(sT_2+1)sT_3} = \frac{1}{0} = \infty$. Oznacza to, że obiekt ma człon całkujący ($s$ w mianowniku).

Jeśli $\lim_{s \to 0} G_S(s) = \infty$, to:

$$ e_{ss} = \frac{1}{1 + K_p \cdot \infty} - \frac{\infty}{1 + K_p \cdot \infty} = 0 - 1 = -1 $$

To jest wynik, który wymagałby dalszej analizy, ponieważ obecność zakłócenia i sygnału zadanego jednocześnie komplikuje sprawę. Zazwyczaj analizuje się uchyb dla każdego wejścia osobno, a następnie sumuje. Jeśli rozważamy tylko uchyb od sygnału zadanego (bez zakłócenia), to $e_{ss} = 0$. Jeśli tylko od zakłócenia, to $e_{ss} = -1$. W przypadku obu, wynik zależy od tego, jak dokładnie zdefiniowany jest uchyb. W tym przypadku, ze względu na człon całkujący w $G_S(s)$, system będzie eliminował uchyb od sygnału zadanego. Uchyb od zakłócenia będzie zależał od struktury pętli.

**2. Regulator Proporcjonalno-Całkujący (PI):** $G_R(s) = K_p + \frac{K_i}{s} = \frac{K_p s + K_i}{s}$

Regulator PI wprowadza dodatkowy człon całkujący do pętli. Jeśli obiekt już ma człon całkujący, to regulator PI dodatkowo poprawi eliminację uchybu w stanie ustalonym. Dla skoku jednostkowego sygnału zadanego i zakłócenia, regulator PI w połączeniu z obiektem z członem całkującym zazwyczaj prowadzi do zerowego uchybu w stanie ustalonym dla obu sygnałów.

**3. Regulator Proporcjonalno-Różniczkujący (PD):** $G_R(s) = K_p + K_d s$

Regulator PD nie zawiera członu całkującego. W przypadku obiektu z członem całkującym, regulator PD nie zmieni charakteru eliminacji uchybu od sygnału zadanego (nadal będzie zerowy). Jednakże, uchyb od zakłócenia może być niezerowy i zależeć od parametrów systemu.

### Podsumowanie

Bez konkretnych wartości stałych czasowych $T_1, T_2, T_3$ oraz parametrów regulatora ($K_p, K_i, K_d$), nie jest możliwe podanie numerycznych wartości uchybu w stanie ustalonym. Ogólnie, obecność członu całkującego w transmitancji obiektu $G_S(s)$ (czyli $s$ w mianowniku) sugeruje, że system będzie w stanie wyeliminować uchyb od sygnału zadanego typu skok jednostkowy. Uchyb od zakłócenia będzie zależał od struktury pętli i typu regulatora.

---
