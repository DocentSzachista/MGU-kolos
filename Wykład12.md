## Object detection

Po krótce móc zaznaczyć nas oczekiwany obiekt na zdjęciu 

## Instance segmentation 
Zaznaczanie każdego piksela w obiekcie

## Semantic segmentation
Tagowanie każdego pixela na obrazie 


## Zbiór danych

- zapis danych zazwyczaj jako:

```class_id, x, y, width, height```

- COCO najbardziej uzywany 

## Intersection over Union

- wyliczane jako: część wspólna bouding boxów / część eksperta bounding boxa 


Jak to zrobić dla serii danych, jedną liczbą opisać czy jest dobrze czy źle?
**mAP** mean average precision 
- Wyznaczamy średnią i określamy konkretną średnią 

Jak wykrywać obiekty

- okno przesuwne po całym zdjęciu 
- 

Jak zmniejszyć liczbę prostokatów
- wrzucić selecitve search by znaleźć obszary podobnie kolorystycznie 
- i dopiero po nich puszczać prostokąty 
- Zaznaczone prostokąty to ROI 
- Pierwszy model co takiego zrobił to R-CNN (2012)
- wuaczymy svm'a wykrywac bounding boxy 
- uczono binarnie 

## Bounding Box Regressor



Wady R-CNN
- długo się liczy
- rozwalenie na kilka sieci 



## Jak to zrobić szybciej 
1. 
- przepuszczać sieć jednokrotnie
- Użycie receptive field i różnowymiarowych konwolucji nałożonych na siebie. 
- Przejść z obrazka na obszar cech . Przechodzimy do ostatniej warstwy konwolucji i mieć wyciągnięty tylko ten obszar co nas interesuje. 

- podejscie 
    - obrazek przepuszczany przez siec konwolucyjna
    - wyciagamy ostatnia warstwe sieci konwolucyjnej
    - wyliczamy z niej ROI 
    - tutaj przeprowadzamy analizę czy mamy obiekt 
2. Jak znaleźć szybciej  obszary zainteresowań  
- Wytrenować sieć która będzie proponować rejony zainteresowań 
- Hasło Region Proposal network 
- Proces teraz wygląda tak
  -> puszczamy obrazek przez siec i dostajemy ostatnią warstwę konwolucji 
  -> puszczamy to do drugiej podsieci która generuje ROI 
  -> Wynik jest zwracany do pierwszej sieci która przeprowadza na bazie tego rozpoznania, następnie zwracane są bounding boxy i rozpoznany obiekt 


## C zrobić gdy dostaniemy za dużo bounding boxów
- Non Maxiumum Suppresion 
    - patrzymy czy wszystkie bounding boxy mają tą samą klasę
    - Wybieramy ten który ma największą pewność po softmaxie
    - resztę usuwamy 


## YOLO (Look bo nie live)

- dzielenie obrazku na sekcje 
- dla każdej ramki trzeba proponować co w niej się znajduje. 
- zaznaczamy ramki z odpowiednim znacznikiem pewności (confidence score)
- zozstawiamy to co ma duże CS i tyle


## v2
- poprawiono sieć o kilka rzeczy


## v3
- zastosowanie połączen rezydualnych
- dodanie dodatkowego wyjścia wcześniej by umieć rozróżniać wielkość elementów, wcześniejsze iteracje sobie z małymi obiektami nie radziły  





 openmmlab 

 jakie miał problem fast r-cnn 