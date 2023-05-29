#

## Świat algorytmów #1

Zajec/Sword


Każdy z Was na pewno choć raz grał w grę w której przeciwnikiem jest komputer. Czy kiedykolwiek ktoś z Was zastanawiał się w jaki sposób komputer potrafi "myśleć"? Czy ktokolwiek z Was próbował sam napisać program który by symulował sztuczną inteligencję? Jeśli nie to polecam każdemu programiście ten temat. W przeciągu kilku lat napisałem dwie gry które symulują sztuczną inteligencję a do trzeciej jedynie wymyśliłem założenia. Tymi grami jest jako taki "Banzai" i syfny "Sexquix" oraz gra którą niedawno ukończyłem (nie ma jej jeszcze w sprzedaży) "StecMen". Wszystkie z w/w gier symulują sztuczną inteligencję. W jaki sposób one to robią opiszę w niniejszym artykule.

Podstawą do napisania programu który będzie symulował "sztuczną inteligencję" jest napisanie dobrego algorytmu. Co to takiego jest ten algorytm postaram się na prostym przykładzie wytłumaczyć.

Algorytm to ciąg instrukcji i poleceń napisanych w dowolnym języku programowania (i na dowolnym komputerze) które w oparciu na danych wejściowych (podanych przez użytkownika programu ) obliczają przy pomocy mniej lub bardziej złożonych obliczeń czysto matematycznych dane wyjściowe, które dają odbiorcy złudzenie że ma do czynienia z istotą rozumną.

Żeby bardziej przybliżyć czytelnikowi problem podam zasadę działania algorytmu użytego w grze "Sexquix" i wytłumaczę dlaczego nie można z nim wygrać (prawie!).

Pisząc tą grę nie miałem jeszcze pojęcia o algorytmach (i dziś wcale nie uważam się za eksperta, lecz na pewno dziś więcej wiem na temat niż wtedy). Problem przed którym stanąłem pisząc tą grę potraktowałem dość pochopnie i dlatego gra wyszła tak a nie inaczej. Komputer w tej grze ma za zadanie udawać inteligentną istotę która potrafi dobrze grać w "kółko i krzyżyk".

Inteligencja w tej grze symulowana jest w następujący sposób:

W pamięci komputera jest 9 bajtów (tu pod adresem $0600-$0609), które przed każdą rozgrywką są zerowane. Każdemu bajtowi przyporządkowane jest odpowiednie miejsce w "kratce". Każdy ruch gracza jak również komputera odhaczany jest w pamięci. Ruch komputera oznaczany jest 1 a gracza 2, wolne pole 0. I tak poniższe pole...

```
     X |  |
     --------
     X |  | O
     --------
     O |  |
```

będzie wyglądać w pamięci 1,0,0,1,0,2,2,0,0

Cyfry czytamy kolejno od lewego górnego rogu w prawo aż do dolnego lewego rogu. W przypadku gry w "kółko i krzyżyk" problem jest dosyć prosty bo wystarczy zapisać w programie wszystkie możliwości i podać oczekiwane odpowiedzi (ta metoda jest w tym przypadku najprostsza lecz nie ma wiele wspólnego z algorytmem).

Problem się o wiele bardziej skomplikował podczas pisania gry "Banzai". Tutaj zasady gry są takie same jak w "kółku i krzyżyku" lecz pole jest o rozmiarach 20x20 oczek. Tutaj zapisanie wszystkich możliwości jest nonsensem z trzech podstawowych przyczyn:

Nie przewidzimy wszystkich możliwości
Zabraknie nam pamięci do ich zapisania
Czas odpowiedzi byłby dość długi


I co w takim przypadku? Oczywiście rozwiązań tego problemu jest wiele lecz ja opiszę tylko ten który sam wymyśliłem lecz jego realizacją programową zajął się 2obert Szurała (ROBUŚ). Przyjmijmy identyczne oznaczenia jak w poprzednim przykładzie (tj. 0-puste oczko, 1-kółko, 2-krzyżyk).

W pamięci mamy wygospodarowany obszar 400 bajtów jako "bufor" pola gry (400 dlatego że pole gry ma 20x20 oczek a 20*20=400). Zaczyna grę gracz. Wprowadza on dane wejściowe w postaci współ. (X,Y), w które umieszczamy kółko (symbol ruchu gracza). Kółko zostaje pokazane na ekranie i odznaczone w pamięci. Adres w który go odznaczam wyliczam z prostego wzoru:

	Adres=Adres_Bufora+Y*20+X

dlatego, że maksymalna ilość wierszy (pionowo) jest 20. Gdy mam wyliczony adres sprawdzam najpierw czy nie ma tam wartości różnej od 0. Jeśli jest, nie zezwalam wstawić tam graczowi kółka. Jeśli nie ma wstawiam tam symbol kółka (czyli 1).

Następnie wyliczam adresy pól położonych nad, pod, obok i pod kątem. Sposób obliczeń jest prosty... dla pola nad adr=adr-20, dla pola pod adr=adr+20, dla pola z lewej adr=adr-1, pola z prawej adr+1 i pod kątem odpowiedni +19, +21, -19, -21. Po wyliczeniu adresu sprawdzam wartość która jest przetrzymywana pod wskazanym adresem. Jeśli jest to 0 (puste oczko) lub 2 (krzyżyk, czyli oznaczenie komputera) anuluję. Natomiast gdy pod wyliczonym adresem znajduje się wartość 1, zapamiętuję w tablicy (adres oraz kierunek). Gdy tak "rozejrzę się w około" patrzę do tablicy z adresami i zapamiętuję adres który tam jest jako pierwszy po czym go "wywalam" z tablicy. W bajcie o zapamiętanym adresie "rozglądam" się lecz tylko we wcześniej zapamiętanym kierunku. Sprawdzam czy tam nie występuje wartość 1. Jeśli tak do zmiennej KROK dodaję 1 i czynność powtarzam ponownie tzn. wyliczam ponowny adres który mieści się dalej w zapamiętanym kierunku; sprawdzam wartość; jeśli jest 1 to liczę nowy adres itd., aż do momentu gdy wartość zmiennej KROK nie wyniesie 6 (takie są akurat założenia gry "Banzai", wartość KROK oznacza ile już gracz postawił kółek obok siebie w jednym kierunku. Tu liczba 6 oznacza wygraną gracza). Jeśli wartość jest już wysoka tj.4 czyli graczowi wystarczy postawić po jednym kółku z jednej i drugiej strony należy natychmiast się zastawiać i wstawiać w tym miejscu krzyżyk w przypadku wartości 5, w zmiennej KROK zastawianie się nie ma już w prawdzie jakiegokolwiek sensu gdyż gracza od wygranej dzieli jeden ruch lecz daje to złudzenie rozpaczliwej obrony bardzo charakterystycznej dla istot rozumnych. Wartość 6 w zmiennej KROK oznacza niewątpliwą wygraną gracza.

Opisany algorytm został przedstawiony w dość schematyczny sposób jeśli ktoś jest zainteresowany powyższym tematem polecam mu książkę napisaną przez pana Piotra Wróblewskiego pt:"ALGORYTMY struktury danych i techniki programowania" - wydawnictwa "Helion" (cena około 30zł).

Książka ta opisuje problemy algorytmiki z przytoczeniem przykładowych rozwiązań w języku C++ na komputer PC. Pomimo tego temat ten jest ogólny dla wszystkich komputerów i pomysły na rozwiązanie wielu problemów przedstawione w tej książce można przetłumaczyć na każdy język programowania "może oprócz logo !!!".

Zajec/Sword


## Jak stworzyć ciekawe efekty

Zajec/Sword


Witam wszystkich zainteresowanych pisaniem dem i intr. Sam nie znam się na asemblerze lecz wiem jak większość efektów jest zrobiona od strony teoretycznej. Pierwszym opisanym przeze mnie efektem jest ...

### Animacja wektorowa 2D

Gdy chcemy zrobić animację wektorową w dwóch wymiarach to musimy użyć do obrotu punktu wzór z pierwszej klasy szkoły średniej:

```
Xr=X0+(X-X0)*cosA+(Y-Y0)*sinA
Yr=X0+(Y-X0)*cosA+(X-Y0)*sinA
```

gdzie:

| Etykieta | Opis                          |
|----------|-------------------------------|
|X0, Y0    | współrzędne punktu obrotu     |
|X, Y      | współrzędne obracanego punktu |
|A         | kąt o jaki obracamy           |
|Xr, Yr    | współrzędne punktu po obrocie |

Powstaje pytanie skąd w asemblerze wziąć wartości sinusa i cosinusa kąta. Otóż potrzebne liczby umieszczamy w tablicy. Do wykonania tablicy można wykorzystać program w języku wyższego poziomu np. Turbo Basicu.

### Animowany lejek

Ten efekt przedstawia animowane okręgi "schodzące" do wewnątrz lejka lub "rozchodzące" się z zewnątrz lejka. Efekt jest niczym innym jak animacją na kolorach a animację uzyskuje się poprzez złudzenie optyczne. Podstawową sprawą jest stworzenie takiego rysunku aby na nim była możliwość animacji na kolorach. Rysunek taki najłatwiej stworzyć w Turbo Basicu dlatego też poniższy program który tworzy "lejek" został napisany w Turbo Basicu.

```
10 GRAPHICS 15:C=1:R=96:X0=79:P=2:CC=1
12 FOR YO=191 TO 95 STEP -1:COLOR C
14 CIRCLE XO,YO,R:C=C+1:R=R-1
16 IF C=4 THEN C=1
18 NEXT Y0:P=2
20 RESTORE 28:FOR Q=0 TO 2:READ A,B,C
22 D=CC*16:A=A+D:B=B+D:C=C+D
24 POKE 708,A:POKE 709,B:POKE 710,C
26 PAUSE P:NEXT Q:GOTO 20
28 DATA 2,4,6,4,6,2,6,2,4
```

Zmieniając wartość 'P' zmieniamy prędkość animacji, natomiast parametrem 'CC' zmieniamy kolor lejka animowanego (tutaj 1 kolor szary). Niedokładności w rysunku czarne pixle można zmniejszyć dopisując linie

	13 CIRCLE X0,Y0,R-1

Lecz najlepiej pozostałe czarne pixele zamalować ręcznie pod dowolnym programem graficznym.

### Rozmycie obrazu

Można uzyskać bardzo prosto, wystarczy uśrednić kolor wszystkich pixeli na ekranie, tzn. kolor pixela o wsp. X,Y równy jest średniej arytmetycznej kolorów pixeli, jego otaczających.

### Wyostrzenie obrazu

Uzyskamy podobnie jak rozmycie jedynie z taką zmianą, że kolor pixela o wsp. X,Y równy jest równaniu:

	C=S+(S-W)

gdzie:

| Etykieta | Opis                          |
|----------|-------------------------------|
| S        | stara wartość aktualnego punktu |
| W        | średnia arytmetyczna kolorów punktów bezpośrednio sąsiadujących z aktualnym |
| C        | nowa intensywność koloru aktualnego punktu |


### Animacja nieskończenie wielu obiektów tzw. "Bobs-y"

Aby uzyskać tzw. bobsy należy umieć wyświetlić szybko kulę na ekranie w trybie $0E Antica (gdyż on najlepiej nadaje się do tego efektu). Kulę oczywiście rysujemy sobie sami w dowolnym programie graficznym, a jej rozmiary nie powinny przekroczyć 16x16 pixeli. Następnym krokiem jest ułożenie sobie tablicy sinusów i cosinusów. Teraz zostaje nam napisać tylko program. Kula ma poruszać się po dowolnej krzywej, którą najlepiej wyliczyć ze wzoru Lisa-żu, który brzmi:

```
Xn=int(sin(X*3.14/180)*R)+W
Yn=int(cos(Y*3.14/180)*R)+W
```

gdzie:

| Etykieta | Opis                          |
|----------|-------------------------------|
|Xn        | nowa pozycja x |
|Yn        | nowa pozycja y |
|X         | stara pozycja x |
|Y         | stara pozycja y |
|R i W     | parametry dowolne(>0 i <100) od których zależny jest przebieg krzywej |

Jeżeli już wyliczyliśmy nowe X i Y dla kuli, teraz musimy znaleźć w pamięci komputera miejsce na 4 ekrany po czym rysujemy kulę o wsp. X,Y na ekranie 1, obliczamy nowe X,Y, przełączamy na 2 ekran i rysujemy kule o nowych wsp. X,Y ponownie obliczamy X i Y, przełączamy na 3 ekran, liczymy ponownie X,Y przełączamy na 4 ekran i rysujemy, liczymy nowe X,Y i przełączamy na 1 ekran i tak w kółko...

### Animacja - morphing punktowy

Morphing punktowy polega na płynnym "przechodzeniu" jednej figury punktowej w drugą. Przed wykonaniem animacji liczymy dla każdego punktu

```
dx = (x2 - x1) / ik
dy = (y2 - y1) / ik
```

gdzie:

| Etykieta | Opis                          |
|----------|-------------------------------|
| (x2,y2)  | punkt docelowy |
| (x,y)    | punkt przechodzący |
| dx,dy    | przyrosty dla współrzędnych punktu, na każdy krok animacji |
|ik        |(ile kroków) ilośc kroków animacji

W czasie animacji wykonujemy kolejno:

1. Zetrzyj punkt (x,y)
2. Policz: x=x+dx, y=y+dy
3. Postaw punkt (x,y)

Operacje 1-3 wykonujemy (ik) razy.

Oczywiście zakładam, że ma się napisaną szybką procedurę stawiania punktu na ekranie, która to jest podstawą dla tego efektu.

Na tym efekciku zakończę
ten artykuł.

Zajec/Sword



