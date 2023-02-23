# Automatyczna drylownica do wiśni
Automatyczna drylownica do wiśni jest tematem pracy dyplomowej inżynierskiej autorstwa Bartosza Mokrzeckiego oraz Sławomira Lida, obronionej na Politechnice Poznańskiej w roku akademickim 2020/2021, prowadzonej przez Dr Hab. inż Pawła Drapikowskiego.

## Praca dyplomowa
Kompletna praca dyplomowa (plik _"Praca_Inżynierska_Sławomir_Lida_Bartosz_Mokrzecki.pdf"_) jest dostępna w tym repozytorium.

# Wideo instruktażowe
[Prezentacja w serwisie YouTube](https://www.youtube.com/shorts/l-_eOu30rVU)

# Dokumentacja
Wiśnie pod wpływem grawitacji wpadają do **bębna z otworami**, którym obraca **sterowany silnik krokowy**.
Wiśnie przemieszczają się do właściwej pozycji gdzie zostaną wydrążone przez **element**
**wyciskający** operowany **serwomechanizmem**, który jest sterowany **mikrokontrolerem STM32F103RB**.
Pestki wypadają od wewnętrznej strony bębna na metalową zwężaną blachę aby trafić do pojemnika
na nie przeznaczonego. Wrzeciono podnosi się, wiśnia zostaje ściągnięta z pomocą blachy po
czym wędruje otworem w bębnie do czasu aż pod wpływem grawitacji wypadnie na metalową
rynnę. Gdy wszystkie wiśnie zostaną wydrążone albo podajnik zostanie zapchany, system
dwóch czujników poinformuje mikrokontroler aby ten mógł zasygnalizować dane zgłoszenie
przez informację na **wyświetlaczu LCD**, zmianę koloru **diody LED** oraz włączenie **sygnału**
**dźwiękowego**. Po zniwelowaniu ewentualnej awarii należy użyć przycisku widocznego na
czerwonym pojemniku służącym jako skrzynka elektryczna. Przybliżoną masę wydrążonych
wiśni można odczytać na wyświetlaczu LCD. Wszystkie elementy zamocowane są na specjalnej
konstrukcji aluminiowych profili. Wspomniany bęben jest przykręcony do stalowego wału, który
pracuje w plastikowym wsporniku. Napędzany jest poprzez **układ przekładni zębatych**.
Mikrokontroler oraz sterownik silnika krokowego umieszczone są we wspomnianym
plastikowym zamykanym pojemniku, umocowanym na profilu aluminiowym. W pokrywie
pojemnika umieszczony został wyświetlacz LCD, wspomniany **przycisk resetujący działanie**
**układu**, dioda LED oraz wyłącznik całego układu.


![Screenshot_12](https://user-images.githubusercontent.com/56951671/220371800-f2b0219b-af2e-49f2-9888-eb59a4d9174d.png)
## Widok główny urządzenia w programie Inventor
![Screenshot_3](https://user-images.githubusercontent.com/56951671/220366961-2958f518-210b-4c0c-a89d-e7ddf85235cd.png)

## Elektronika
![Screenshot_1](https://user-images.githubusercontent.com/56951671/220367771-70409d35-26dc-4dae-b0b0-a2dcd63d6571.png)

## Schemat ideowy układu
![Screenshot_2](https://user-images.githubusercontent.com/56951671/220367938-4c64fa8c-4174-4397-ab2b-07ade8f75d08.png)

## Projekt płytki drukowanej
![Screenshot_4](https://user-images.githubusercontent.com/56951671/220368094-9486d57b-b4b3-4485-a0fe-cb6cc2d5cbf0.png)

## Algorytm działania programu
![Screenshot_5](https://user-images.githubusercontent.com/56951671/220368392-a353c04a-61a4-43c9-b7aa-94bacf36175a.png)

Działanie silnika krokowego w nieskooczonej pętli głównej:
![Screenshot_6](https://user-images.githubusercontent.com/56951671/220368576-faf1e9f1-9237-4b0b-80f5-f7eafcc7eb5a.png)

Pierwszy z warunków dotyczący obecności wiśni pod wrzecionem sygnalizowany barierą podczerwieni.
![Screenshot_7](https://user-images.githubusercontent.com/56951671/220368697-68a2a664-3f22-4293-bf5e-6cf085e4c1d9.png)

Drugi z warunków dotyczący obecności wiśni w bębnie, sygnalizowany czujnikiem
przerwania wiązki IR oraz sama funkcja wyciskająca wiśnie z użyciem serwomechanizmu.
Zmienna “cherry” to licznik sumujący przybliżoną masę wiśni, po każdym wyciśnięciu wrzeciona.
Funkcja “__HAL_TIM_SET_COMPARE” odpowiada za ruch serwomechanizmu, po obliczeniu
częstotliwości, na której pracuje serwomechanizmy i znalezieniu odpowiednich wypełnieo
sygnału. Ustawiając wypełnienie na 600 poruszamy się serwomechanizmem do pozycji
początkowej, odczekujemy sekundę, aż ruch się wykona. Na wypełnieniu 2400 następuje pełny
obrót serwomechanizmu o 180°, po wyciśnięciu pestki serwomechanizm powraca do pozycji
początkowej. Na końcu zmienna warunkowa jest resetowana aby móc poprawnie wykonać
kolejny cykl pracy. 
![Screenshot_8](https://user-images.githubusercontent.com/56951671/220368805-4817e768-f167-42b5-b5d7-d71be3ef38cc.png)

Zastosowany został system zabezpieczenia oparty na dwóch użytych czujnikach. Jeśli
czujnik przerwania wiązki wykryje, że wiśnia nie znajduje się w bębnie oraz wiązka czujnika
szczelinowego nie jest przerwana, zostaje inkrementowana zmienna “licznik” zliczająca takie
impulsy.
![Screenshot_9](https://user-images.githubusercontent.com/56951671/220370197-585e9fd3-9e8a-43c2-a586-6751af944966.png)

Gdy zmienna ta przekroczy wartośd 3, praca silnika krokowego zostaje zatrzymana,
zostaje uruchomiony ostrzegawczy sygnał dźwiękowy, kolor sygnalizacyjnej diody LED zostaje
zmieniony z czerwonego na zielony, zmienna “licznik” a na wyświetlaczu LCD zostaje
wyświetlona informacja o awarii lub braku wiśni. Układ wraca do właściwej pracy po wciśnięciu
przycisku na obudowie skrzynki elektronicznej. 
![Screenshot_10](https://user-images.githubusercontent.com/56951671/220370327-391ddfa2-7cdf-4ddd-81df-26bb823d684c.png)

Po włączeniu całego układu na wyświetlaczu LCD wyświetla się nazwa urządzenia, a po
trzech sekundach zostaje wyświetlana przybliżona masa wydrążonych wiśni. 
![Screenshot_11](https://user-images.githubusercontent.com/56951671/220370408-3f5b122c-9d01-4ddd-921a-44ebb0e710c4.png)
