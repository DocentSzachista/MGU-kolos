## IOT modele 


## Jak sprawić by model działał na mobilce?

## Problemy
- mniejsza moc obliczeniowa
- chcemy jak najszybciej by to działało
- moc baterii

## Rozwiazania
- Wysyłać na serwer
- Zmniejszyć rozmiar modelu



## SqueezeNet (2016)
- wykorzystanie konwolucji 1x1 by zmniejszyć ilość kanałów (rozmiar sieci) i szybciej przetwarzać dane
- 

## MobileNet (2017)
- Zastosowanie najpierw depthwise convolution i potem pointwise convolution (czyli 1x1)
- Wykorzystanie strife'u do gradientu


## Relu6
<!-- TODO: Wrzuć wykresik  -->
- ma być bardziej precyzyjne. 


## MobileNet v2 (2018) 
- połączenia rezydualne (Gradient gradient gradient...)
- najpierw pomniejszać liczbę kanałów a potem ją znowu powiększać. 


## Mobilenet v3
- dodanie liczenie wag z Seneta
- zmiana global average pooling i linear na jedną konwolucję 1x1 zwracającą 1000 klas 

## GhostNet 
- idea: przerzucamy część danych z konwolucji do wyjścia?? // wklep w gpt4 
- 



## Deployment na mobilki 

