Modele generatywne 

Model działania GAN'u 

- Dyskryminator 
- generator


Można używać gotowych struktura ale nie wyuczonych XD

lepsze jest SIMClr


Jak ocenić GAN?

- Patrzymy po tym jak obrazki są generowane po prostu 
- Frechet Inception Distance

- mamy rozkład danych sztucznych i prawdziwych i porównujemy te rozkłady z poziomu cech. Wykorzystuje się do tego Inceptoon v3. Daleko to źle oszukaliśmy, blisko, to dobrze.

- minusy: 
- sieć neuronowa
- 


## DCGAN - 2016


Jak generować konkretną cyfrę? 
- Conditional GAN - przyjmowanie jakiegoś y'ka by wiedział że jest to np pies i uczył się rozrózniać


## Wasserstein GAN - 2017 
- dyskryminator zwraca teraz informację o tym jak bardzo źle jest generowane bądź dobrze. 


## BiGAN /AliGAN 
- Teraz dodajmy jeszcze wektory cech do generatora. (Za pomocą encodera)
- lepsze zrozumienie szumu, dzięki czemu jesteśmy w stanie lepiej określić detale w wygenerowanym obrazku 

## CycleGAN  - 2017  
- Zmieniamy style w obrazkach
- jeden generator tworzy jakiś szum, który drugi generator próbuje odtworzyć
- dyskriminatorem jest Unet 
- Kontrolujemy jeszcze w postaci 2 dyskryminatorów: 1 do stylu drugi do oryginału obrazka. 

## PixToPix
