# Predykcja Wartości Rynkowej i Bankructwa Amerykańskich Firm

## Opis Projektu
Projekt skupia się na analizie danych finansowych amerykańskich firm w celu przewidywania ich przyszłej wyceny giełdowej oraz oceny ryzyka bankructwa. Do analizy wykorzystano modele uczenia maszynowego (regresję liniową oraz regresję logistyczną), które oceniają kondycję firmy w roku $t+1$ na podstawie wskaźników z roku $t$.

---

## Technologie i Biblioteki
* **Pandas**: Pobieranie, organizacja i manipulacja danymi.
* **NumPy**: Zaawansowane obliczenia numeryczne.
* **Matplotlib**: Wizualizacja wyników, w tym wykresów korelacji oraz macierzy błędów.
* **Scikit-learn**: Dzielenie danych (`train_test_split`), trenowanie modeli (`LinearRegression`, `LogisticRegression`) i obliczanie metryk jakościowych.
* **Kaggle API**: Bezpośrednie pobieranie źródłowego zbioru danych w środowisku Google Colab.

---

## Zbiór Danych
Do analizy wykorzystano zasób "American Companies Bankruptcy Prediction Dataset", składający się z 78682 rekordów. Tabela poniżej przedstawia kluczowe zmienne wykorzystane w projekcie:

| Zmienna | Opis |
| :--- | :--- |
| **X1-X18** | Cechy numeryczne definiujące wskaźniki finansowe, takie jak Aktywa obrotowe (X1), EBITDA (X4) czy Całkowite zadłużenie (X11). |
| **X8** | Wartość rynkowa (kapitalizacja giełdowa) wykorzystywana jako zmienna docelowa w analizie predykcyjnej sukcesu. |
| **status_label** | Etykieta określająca bieżący status przedsiębiorstwa (klasy *alive* i *failed*). |
| **year** | Rok pomiaru historycznych danych finansowych. |

---

## Realizowane Zadania i Wyniki

### 1. Predykcja Sukcesu (Regresja)
* **Cel**: Prognozowanie przyszłej wartości rynkowej firmy (X8) z rocznym wyprzedzeniem.
* **Model i Dane**: Wykorzystano klasyczną regresję liniową, trenując ją na 55768 próbkach i testując na 13943 obserwacjach.
* **Precyzja Modelu**: Wykazano niezwykle wysoką predykcyjność bieżących danych, co potwierdza wskaźnik dopasowania R^2 na poziomie 0.9525.
* **Istotność Cech**: Analiza korelacji wykazała, że poza samą wyceną bazową, wskaźniki rentowności takie jak EBITDA (X4) oraz EBIT (X12) są najmocniejszymi czynnikami określającymi przyszły wzrost wyceny.

### 2. Przewidywanie Bankructwa (Klasyfikacja)
* **Cel**: Przewidzenie upadku firmy (`status_label` = *failed*) w roku następującym po analizowanym okresie.
* **Model i Dane**: Zastosowano model regresji logistycznej z parametrem `class_weight='balanced'`, dzieląc dane w sposób zachowujący naturalne, niezbalansowane proporcje klas (stratyfikacja).
* **Wykrywalność Upadków (Recall)**: Wskaźnik czułości wyniósł 85% dla klasy *failed*, co świadczy o wysokiej skuteczności wychwytywania przez algorytm firm faktycznie zmierzających do bankructwa.
* **Precyzja Alarmów (Precision)**: Metryka Precision ustabilizowała się na niskim poziomie 8%, obniżając ogólną dokładność modelu (36%) i generując znaczny odsetek fałszywych alarmów.
* **Wnioski Biznesowe**: Pomimo niskiej precyzji, zbalansowanie wag naprawiło główny błąd ignorowania klasy mniejszościowej i pozwoliło stworzyć czuły system wczesnego ostrzegania w zarządzaniu ryzykiem. Preferuje on podwójną weryfikację nad błąd przeoczenia.

---

## Uruchomienie Projektu
1. Otwórz notatnik `.ipynb` w chmurze obliczeniowej (rekomendowane środowisko: Google Colab z akceleratorem T4 GPU).
2. Skonfiguruj klucze API Kaggle (zmienne środowiskowe `KAGGLE_USERNAME` oraz `KAGGLE_KEY`), aby środowisko mogło samoczynnie pobrać zbiór danych w pierwszych komórkach uruchomieniowych.
