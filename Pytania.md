## Kiedy chcemy skupić się na wyciąganiu wzorców lepiej ejst zastosować AveragePooling czy MaxPooling?

## Po co kilka konwolucji pod rząd
Dwie konwolucje 3x3 działają podobnie jak jedna 5x5, ale przy dwóch konwolucjach mamy do zapamiętania mniej informacji, a oprócz tego mamy możliwość wciśnięcia dodatkowej funkcji aktywacji
## Po co stosować konwolucję 1x1
Pozwala tanim kosztem manipulować liczbą kanałów - np ze 100 zrobić 1. Wyciąga kluczowe cechy z wielu warstw.

## Jak liczyć forward pass?
Przeprowadzać normalne obliczenia na macierzach, w zależności od operacji. Na przykład na konwolucji wykonywać mnożenia.

## Jak liczyć backpropagation?
Poprzez pochodne cząstkowe.

## Czemu nie ma konwolucji parzystych 2x2, 4x4, 6x6
Nie robi się konwolucji parzystej, bo kwadraty wtedy nie mają środka. Samą operacje teoretycznie dałoby się wykonać, ale byłby problem z określeniem gdzie wpisać wynik konwolucji - kombinowanie.



## Jakie jest zastosowanie konwolucji 1x1
- Zmiana liczby kanałów: Konwolucja 1x1 może zmieniać liczbę kanałów w mapie cech. Na przykład, jeśli wejściowa mapa cech ma 256 kanałów, a chcemy zredukować je do 64, używamy konwolucji 1x1 z 64 filtrami. To pozwala na zmniejszenie złożoności modelu i jego wymagań obliczeniowych.
- Zwiększenie nieliniowości: Pomimo swojej prostoty, konwolucje 1x1 wprowadzają dodatkową nieliniowość do modelu, gdy są stosowane z funkcjami aktywacji, takimi jak ReLU. To pomaga w wyłapywaniu bardziej skomplikowanych wzorców w danych.
- Efektywna integracja informacji z różnych kanałów: Konwolucja 1x1 efektywnie łączy informacje z różnych kanałów mapy cech. Dzięki temu model może lepiej uczyć się zależności między kanałami.

## Po co stosować podwójną konwolucję
- Lepsze Wyłapywanie Cech: Stosowanie dwóch konwolucji po sobie pozwala modelowi na wyłapywanie bardziej złożonych cech w danych. Pierwsza warstwa może wyłapywać proste wzorce, takie jak krawędzie czy kolory, a druga warstwa może integrować te proste wzorce w bardziej skomplikowane struktury.

- Zwiększenie Głębokości Sieci bez Nadmiernego Zwiększania Złożoności: Przez stosowanie wielu lżejszych warstw konwolucyjnych zamiast jednej ciężkiej, można zwiększyć głębokość sieci bez znacznego wzrostu liczby parametrów i obciążenia obliczeniowego.

- Nieliniowość i Abstrakcja: Między warstwami konwolucyjnymi często stosuje się funkcje aktywacji (np. ReLU). Dzięki temu system może wprowadzać nieliniowość do procesu uczenia, co jest kluczowe dla efektywnego modelowania złożonych relacji w danych.

- Zastosowania w Sieciach Segregacyjnych: W sieciach służących do segmentacji obrazów, takich jak U-Net, podwójne konwolucje są wykorzystywane do stopniowego zmniejszania wymiarów przestrzennych, jednocześnie zwiększając liczbę cech. To pozwala na efektywną analizę i klasyfikację różnych regionów obrazu.

- Ograniczenie Przesadnego Dopasowania: Stosując dwie lub więcej warstw konwolucyjnych zamiast jednej dużej, można potencjalnie zmniejszyć ryzyko przeuczenia się (overfitting) sieci do danych treningowych, co jest szczególnie ważne w zadaniach z ograniczoną ilością danych.


## Zastosowanie funkcji flatten i jaki jest Jego zamiennik
### Flatten:
- Przekształcanie Map Cech na Wektor: flatten służy do przekształcenia wielowymiarowych map cech (wynikających z warstw konwolucyjnych i poolingowych) na jednowymiarowy wektor. Jest to kluczowe, ponieważ warstwy w pełni połączone (fully connected layers), które zwykle następują po warstwach konwolucyjnych, wymagają danych wejściowych w formie jednowymiarowej.

- Przygotowanie do Klasyfikacji: Po przetworzeniu obrazu przez warstwy konwolucyjne i poolingowe, flatten umożliwia przekształcenie wynikającej z tego mapy cech na format, który może być użyty do klasyfikacji (np. rozpoznawanie obiektów na obrazie).

### GlobalAveragePooling
- stosowane jako alternatywa do warstwy Flatten
- Redukcja Parametrów: GAP znacznie redukuje liczbę parametrów, przekształcając każdą mapę cech w pojedynczą liczbę przez obliczenie średniej wartości wszystkich jej elementów. Dzięki temu zmniejsza ryzyko przeuczenia (overfitting).

- Utrzymanie Przestrzennych Informacji: W przeciwieństwie do flatten, GAP zachowuje przestrzenną informację o cechach, co jest ważne w niektórych aplikacjach, takich jak lokalizacja obiektów na obrazie.
- Elastyczność Rozmiaru Wejściowego: GAP umożliwia sieci radzenie sobie z obrazami o różnych rozmiarach, ponieważ niezależnie od rozmiaru wejściowej mapy cech, wyjście GAP jest stałe (jedna wartość na kanał).

## Auxiliary classifier
## Sieć inception3, szukać odpowiedzi na to jak nie utracić gradientu za pomocą pogłębiania sieci (zastosowanie kroku "skip")
## Po co jest depthwise convolutin
 Depthwise convolution jest to przeprowadzanie konwolucji na każdym pojedynczym kanale koloru w obrazie a następnie połączenie wyników konwolucją 1x1. 
 Zalety:
 - zmniejszona liczba operacji. Mniej operacji mnożenia, gdyż iterujemy po każdym kanale osobno
 - zmniejszona liczba parametrów, co zmniejsza ryzyko przeuczenia się sieci.
## (Ogarnąć) Plusy resnet'a i depthneta
**ResNet**
- Rozwiązanie Problemu Zanikającego Gradientu: ResNet wprowadza połączenia rezydualne, które umożliwiają propagację gradientu wstecz przez wiele warstw, pomagając w treningu bardzo głębokich sieci.
- Możliwość Budowy Głębszych Sieci: Dzięki połączeniom rezydualnym, ResNet umożliwia skuteczne trenowanie sieci o znacznie większej głębokości niż to było możliwe wcześniej (np. ResNet-152).
- Wysoka Skuteczność w Zadaniach Klasyfikacyjnych: Sieci ResNet osiągają bardzo dobre wyniki w zadaniach klasyfikacji i rozpoznawania obrazów.
- Lepsza Generalizacja: Połączenia rezydualne pomagają w generalizacji modelu, co jest korzystne przy przenoszeniu nauczonych cech na nowe, niewidziane dane.

**DenseNet**

- Efektywne Wykorzystanie Parametrów: W DenseNet każda warstwa otrzymuje jako wejście dane z wszystkich poprzednich warstw, co prowadzi do bardziej efektywnego wykorzystania parametrów i zmniejsza ryzyko przeuczenia.
- Ulepszona Propagacja Cech i Gradientów: Dzięki gęstym połączeniom, cechy z wcześniejszych warstw są bezpośrednio przekazywane do późniejszych warstw, co poprawia przepływ informacji i gradientów w sieci.
- Zmniejszenie Zapotrzebowania na Liczbę Kanałów: Gęste połączenia pozwalają na redukcję liczby kanałów w każdej warstwie konwolucyjnej, ponieważ sieć może korzystać z cech zgromadzonych z poprzednich warstw.
- Dobry w Wykrywaniu Detali: Dzięki zachowaniu wszystkich cech z poprzednich warstw, DenseNet jest szczególnie dobry w wykrywaniu drobnych detali w obrazach.