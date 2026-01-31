# Rozwiązanie zadania z kolokwium z Podstaw Automatyki (Wersja Finalna)

---

### Zadanie 1: Schemat blokowy układu sterowania ze sprzężeniem zwrotnym

Schemat blokowy układu sterowania realizowanego za pomocą sprzężenia zwrotnego jest fundamentalnym modelem w teorii sterowania. Poniżej przedstawiono jego typową strukturę wraz z opisem kluczowych sygnałów i elementów.

**Schemat blokowy:**

![Schemat blokowy układu sterowania ze sprzężeniem zwrotnym](https://files.manuscdn.com/user_upload_by_module/session_file/114709955/VmiReEHhaufmbLyl.png)

**Podstawowe sygnały i elementy:**

*   **Sygnały:**
    *   $r(t)$ (**sygnał zadany**, ang. *setpoint*): Wartość pożądana, którą ma osiągnąć sygnał wyjściowy.
    *   $y(t)$ (**sygnał wyjściowy**, ang. *output*): Aktualna wartość wielkości regulowanej, mierzona na wyjściu z obiektu.
    *   $e(t)$ (**sygnał błędu** lub **uchyb regulacji**, ang. *error signal*): Różnica między sygnałem zadanym a zmierzoną wartością sygnału wyjściowego. Oblicza się go jako: $e(t) = r(t) - y_{m}(t)$, gdzie $y_{m}(t)$ to zmierzona wartość wyjścia.
    *   $u(t)$ (**sygnał sterujący**, ang. *control signal*): Sygnał generowany przez regulator, który jest podawany na wejście obiektu sterowania w celu minimalizacji błędu.

*   **Elementy (bloki):**
    *   $C(s)$ (**regulator**, ang. *controller*): Serce układu. Na podstawie sygnału błędu $e(t)$ generuje odpowiedni sygnał sterujący $u(t)$.
    *   $G(s)$ (**obiekt sterowania**, ang. *plant*): System lub proces, którego działanie chcemy kontrolować.
    *   $H(s)$ (**blok sprzężenia zwrotnego** / **czujnik**, ang. *feedback block/sensor*): Element mierzący sygnał wyjściowy $y(t)$ i przekazujący go do węzła sumacyjnego. W najprostszym przypadku (sprzężenie jednostkowe) $H(s) = 1$.
    *   **Węzeł sumacyjny** (`⊖`): Miejsce, w którym sygnał ze sprzężenia zwrotnego jest odejmowany od sygnału zadanego w celu obliczenia błędu regulacji.

---

### Zadanie 2: Etapy projektowania układu sterowania

Proces projektowania układu sterowania jest złożonym zadaniem inżynierskim, które można podzielić na następujące, logicznie uporządkowane etapy:

1.  **Analiza obiektu i specyfikacja wymagań:** Zrozumienie fizycznego procesu, który ma być sterowany. Określa się tu cele sterowania (np. stabilizacja, śledzenie trajektorii) oraz wymagania dotyczące jakości regulacji (np. szybkość odpowiedzi, dokładność).

2.  **Modelowanie matematyczne obiektu:** Stworzenie matematycznego opisu (modelu) zachowania się obiektu. Model ten może mieć postać równań różniczkowych, transmitancji operatorowej, czy też równań stanu.

3.  **Analiza właściwości obiektu:** Badanie modelu w celu zrozumienia jego charakterystyk, takich jak stabilność, dynamika, czy charakterystyki częstotliwościowe.

4.  **Projekt i synteza regulatora:** Wybór struktury regulatora (np. P, PI, PID) i dobór jego nastaw (parametrów) w taki sposób, aby zamknięty układ sterowania spełniał postawione wymagania.

5.  **Symulacja i weryfikacja:** Przeprowadzenie symulacji komputerowych zaprojektowanego układu w celu oceny jego działania w różnych warunkach pracy.

6.  **Implementacja i testowanie:** Wdrożenie algorytmu sterowania w rzeczywistym systemie i przeprowadzenie testów na fizycznym obiekcie.

---

### Zadanie 3: Układ sterowania ekstremalnego

Układy sterowania ekstremalnego mają na celu utrzymywanie pracy obiektu w punkcie, w którym pewien wskaźnik jakości osiąga wartość ekstremalną (maksimum lub minimum).

**Schemat blokowy:**

![Schemat blokowy układu sterowania ekstremalnego](https://files.manuscdn.com/user_upload_by_module/session_file/114709955/ngRbqvDFAkQKayQs.png)

**Przykład:** Optymalizacja procesu spalania w silniku spalinowym. Celem jest znalezienie takiego składu mieszanki paliwowo-powietrznej, przy którym moc silnika jest maksymalna.

---

### Zadanie 4: Analiza transmitancji $G(s) = \frac{s-2}{s+2}$

#### Wprowadzenie dla początkujących: Czym jest dziedzina Laplace'a?

Zanim przejdziemy do rozwiązania, wyjaśnijmy kilka kluczowych pojęć, które są fundamentem tego zadania. Jeśli słyszysz o nich po raz pierwszy, ta sekcja jest dla Ciebie!

**1. Dwa światy: dziedzina czasu i dziedzina Laplace'a**

*   **Dziedzina czasu (to, co widzimy):** To nasz "prawdziwy" świat. Opisujemy w nim, jak sygnały (np. temperatura, prędkość) zmieniają się w funkcji czasu. Używamy do tego funkcji takich jak $f(t)$ i operacji, które mogą być skomplikowane, np. **równania różniczkowe** (które opisują tempo zmian).

*   **Dziedzina Laplace'a (matematyczny "skrót"):** To abstrakcyjny, matematyczny świat, do którego "przenosimy" nasz problem, aby go uprościć. Jest to potężne narzędzie, ponieważ pozwala zamienić trudne operacje (jak różniczkowanie i całkowanie) na proste działania algebraiczne (mnożenie i dzielenie).

**2. Transformata Laplace'a: Bilet w jedną stronę**

**Transformata Laplace'a** to matematyczny "bilet", który pozwala nam przenieść funkcję z dziedziny czasu $f(t)$ do dziedziny Laplace'a, gdzie staje się ona funkcją $F(s)$. Zmienna $s$ jest zespoloną zmienną częstotliwościową, ale na tym etapie wystarczy myśleć o niej jako o "matematycznym zamienniku" dla operacji różniczkowania.

**3. Transmitancja G(s): "Mapa" obiektu w świecie Laplace'a**

**Transmitancja**, oznaczana jako $G(s)$, to opis obiektu sterowania (np. silnika, pieca) w dziedzinie Laplace'a. Jest to po prostu stosunek transformaty Laplace'a sygnału wyjściowego $Y(s)$ do transformaty Laplace'a sygnału wejściowego $U(s)$:

$$ G(s) = \frac{\text{Wyjście}}{\text{Wejście}} = \frac{Y(s)}{U(s)} $$

Dzięki temu, zamiast rozwiązywać skomplikowane równania różniczkowe, możemy po prostu pomnożyć wejście przez transmitancję, aby uzyskać wyjście: $Y(s) = G(s) \cdot U(s)$.

**4. Kluczowa zasada: Różniczkowanie staje się mnożeniem**

Najważniejsza korzyść z transformaty Laplace'a w automatyce to fakt, że operacja **różniczkowania** w dziedzinie czasu (czyli obliczanie pochodnej $\frac{df(t)}{dt}$), w dziedzinie Laplace'a staje się prostym **mnożeniem przez $s$**.

$$ \mathcal{L} \left\{ \frac{df(t)}{dt} \right\} = sF(s) $$

To właśnie ta właściwość pozwala nam zamienić skomplikowane równania różniczkowe na proste równania algebraiczne, co znacząco ułatwia analizę.

#### 4.1. Podać równanie różniczkowe obiektu

**Wyjaśnienie dla początkującego:**

Transmitancja $G(s)$ to "skrócony" matematyczny opis obiektu sterowania w dziedzinie Laplace'a. Jest ona bardzo wygodna do analizy, ale aby zrozumieć, jak obiekt zachowuje się w czasie, musimy wrócić do "normalnego" opisu, czyli równania różniczkowego. Kluczem jest zrozumienie, że operacja mnożenia przez $s$ w dziedzinie Laplace'a odpowiada operacji różniczkowania (obliczania pochodnej) w dziedzinie czasu.

**Krok 1: Zapisanie definicji transmitancji**

Transmitancja to stosunek wyjścia $Y(s)$ do wejścia $U(s)$:

$$ G(s) = \frac{Y(s)}{U(s)} = \frac{s-2}{s+2} $$

**Krok 2: Przekształcenie algebraiczne (pozbycie się ułamka)**

Mnożymy obie strony równania przez mianowniki, aby uzyskać prostszą postać:

$$ Y(s) \cdot (s+2) = U(s) \cdot (s-2) $$

Teraz wymnażamy nawiasy:

$$ sY(s) + 2Y(s) = sU(s) - 2U(s) $$

**Krok 3: Powrót do dziedziny czasu (odwrotna transformata Laplace'a)**

Teraz zamieniamy równanie z powrotem do dziedziny czasu, pamiętając o fundamentalnej zasadzie: $sF(s)$ w dziedzinie Laplace'a to to samo co $\frac{df(t)}{dt}$ (pochodna funkcji $f(t)$) w dziedzinie czasu.

*   $sY(s)$ zamienia się na $\frac{dy(t)}{dt}$
*   $2Y(s)$ zamienia się na $2y(t)$
*   $sU(s)$ zamienia się na $\frac{du(t)}{dt}$
*   $2U(s)$ zamienia się na $2u(t)$

Podstawiając te transformacje do naszego równania, otrzymujemy końcowe **równanie różniczkowe**:

$$ \frac{dy(t)}{dt} + 2y(t) = \frac{du(t)}{dt} - 2u(t) $$

#### 4.2. Narysować jego schemat blokowy

**Wyjaśnienie dla początkującego:**

Schemat blokowy to graficzna reprezentacja równania matematycznego. Aby go narysować, często przekształcamy transmitancję do postaci, która jest łatwiejsza do "zwizualizowania". Dobrą strategią jest rozbicie skomplikowanego ułamka na prostsze części.

**Krok 1: Przekształcenie transmitancji**

Zauważmy, że licznik $(s-2)$ jest podobny do mianownika $(s+2)$. Możemy to wykorzystać, aby uprościć wyrażenie. Dodajmy i odejmijmy 4 w liczniku:

$$ G(s) = \frac{s-2}{s+2} = \frac{(s+2) - 4}{s+2} $$

Teraz możemy rozbić ten jeden ułamek na dwa prostsze:

$$ G(s) = \frac{s+2}{s+2} - \frac{4}{s+2} = 1 - \frac{4}{s+2} $$

**Krok 2: Interpretacja i rysowanie schematu**

Ta nowa postać $G(s) = 1 - \frac{4}{s+2}$ mówi nam, że sygnał wyjściowy $Y(s)$ jest wynikiem dwóch operacji:

1.  Część sygnału wejściowego $U(s)$ przechodzi bezpośrednio na wyjście (gałąź z wartością **1**).
2.  Druga część sygnału wejściowego $U(s)$ jest mnożona przez **4**, następnie przechodzi przez blok $\frac{1}{s+2}$, a na końcu jest **odejmowana** od pierwszej części.

Graficznie wygląda to tak:

![Schemat blokowy transmitancji G(s)](https://files.manuscdn.com/user_upload_by_module/session_file/114709955/SEHzKNcigWwmWOIL.png)

---

### Zadanie 5: Dalsza analiza obiektu

#### 5.1. Charakterystyka statyczna

Charakterystykę statyczną wyznacza się, badając zachowanie obiektu w stanie ustalonym, czyli gdy wszystkie zmiany ustaną. W dziedzinie Laplace'a odpowiada to sytuacji, gdy $s \to 0$.

$$ k = G(0) = \frac{0-2}{0+2} = -1 $$

Wzmocnienie statyczne $k = -1$ oznacza, że w stanie ustalonym wartość na wyjściu będzie przeciwna do wartości na wejściu: $y_{ss} = -u_{ss}$.

**Szkic charakterystyki statycznej:**

![Charakterystyka statyczna](https://files.manuscdn.com/user_upload_by_module/session_file/114709955/CAHrVzEvZdyTuzEW.png)

#### 5.2. Równania stanu i obserwacji

Aby wyznaczyć równania stanu, korzystamy z postaci $G(s) = 1 - \frac{4}{s+2}$.

**Równanie stanu:**

Definiujemy zmienną stanu $x(t)$ poprzez jej transformatę $X(s)$:

$$ \frac{X(s)}{U(s)} = \frac{1}{s+2} \implies sX(s) + 2X(s) = U(s) $$

Po przejściu do dziedziny czasu otrzymujemy **równanie stanu**:

$$ \dot{x}(t) = -2x(t) + u(t) $$

**Równanie wyjścia (obserwacji):**

Wyjście $Y(s)$ to, zgodnie z przekształconą transmitancją, $Y(s) = U(s) - 4X(s)$. W dziedzinie czasu daje to **równanie wyjścia**:

$$ y(t) = u(t) - 4x(t) $$

**Postać macierzowa:**

*   Równanie stanu: $\dot{x}(t) = [-2]x(t) + [1]u(t)$
*   Równanie wyjścia: $y(t) = [-4]x(t) + [1]u(t)$

Co odpowiada macierzom: $A = [-2]$, $B = [1]$, $C = [-4]$, $D = [1]$.
