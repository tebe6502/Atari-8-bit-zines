#

## Jak uniknąć dwubuforowania ?

Piotr Fusik (Fox/Taquart)


Dwubuforowanie (ang. double-buffering) jest techniką pozwalającą uniknąć wyświetlania obrazu, którego tworzenie nie zostało jeszcze ukończone. 
Idea dwubuforowania jest prosta: w pamięci są dwa obrazy, z których jeden jest wyświetlany na ekranie, a drugi tworzony (rysowany). 

Po utworzeniu obrazu zaczynamy go wyświetlać, jednocześnie rozpoczynając rysowanie na obrazie, który dotychczas był wyświetlany. 
Podstawową wadą dwubuforowania jest pamięciochłonność: trzeba przeznaczyć pamięć co najmniej na dodatkowy drugi obraz. 

Zużycie pamięci na implementację dwubuforowania jest jeszcze większe w przypadku rozpętlonego programu, w którym każdy bajt obrazu jest zapisywany inną instrukcją. 
Chcielibyśmy oszczędzić tę pamięc, oczywiście nie wprowadzając migotania obrazu. 

Poniżej opiszę, jak można rysować na jednym obrazie, który jest ciągle wyświetlany, w ten sposób aby rysowanie nie było widoczne.

Podstawowe znaczenie mają dwie rzeczy:

- w jakiej kolejności rysujemy (preferowane jest rysowanie całego obrazu linia po linii z góry na dół)

- jak szybko rysujemy w porównaniu z prędkością wyświetlania

___Rysowanie w dowolnej kolejności___

Pierwszy przypadek jest najbardziej ogólny: obraz jest tworzony przez stawianie pikseli w dowolnej kolejności. 

Jeśli nie chcemy, aby wyświetlił się obraz nie dokończony, musimy zdążyć z narysowaniem go w czasie, gdy obraz nie jest wyświetlany.

```
            -------------------------                    Rys. 1a
            |       poprzedni       |
            -------------------------
rysowanie > |XXXXXXXXXXXXXXXXXXXXXXX|
            -------------------------
            |                       |
    wolne > |       aktualny        |
            |                       |
            -------------------------
            |XXXXXXXXXXXXXXXXXXXXXXX|
```
Rys. 1a pokazuje upływ czasu mierzony w liniach ekranowych. 

Termin "linia ekranowa" został tutaj użyty w znaczeniu jednostki czasu, równej 114 cyklom głównego zegara Atari. 

Oczywiście jest to czas potrzebny na wyświetlenie jednej linii ekranowej. 

Na rysunku został zaznaczony czas, w którym wyświetlany jest obraz (na biało) oraz czas, w którym obraz nie jest wyświetlany (wyświetlana jest ramka lub następuje powrót pionowy - kolor szary). Jak pokazuje rysunek, czasu dostępnego na rysowanie w przypadku jest niewiele. 

W czasie wyświetlania obrazu (na schemacie oznaczenie "wolne") nie możemy nic rysować, możemy natomiast wykonać obliczenia.

___Rysowanie z góry na dół szybsze od wyświetlania___

```
            -------------------------                    Rys. 1b
            |       poprzedni       |
            -------------------------
    wolne > |XXXXXXXXXXXXXXXXXXXXXXX|
            -------------------------
            |                       |
rysowanie > |       aktualny        |
            |                       |
            -------------------------
            |XXXXXXXXXXXXXXXXXXXXXXX|
```

Jeśli w tym przypadku zaczniemy rysować chwilę przed tym, jak obraz zacznie być wyświetlany, zdążymy z jego ukończeniem przed zakończeniem wyświetlania (rys. 1b). 

Przypadek ten jest o tyle ciekawy, że możemy ograniczyć pamięć obrazu do jednej, stale aktualizowanej linii (ew. dwóch). 

Umieszczenie tej linii na stronie zerowej lub na stosie pozwala dodatkowo przyspieszyć rysowanie.

___Rysowanie z góry na dół wolniejsze od wyświetlania___

```
            -------------------------                    Rys. 1c
            |       poprzedni       |
            -------------------------
    wolne > |XXXXXXXXXXXXXXXXXXXXXXX|
            -------------------------
            |                       |
            |       poprzedni       |
            |                       |
rysowanie > |XXXXXXXXXXXXXXXXXXXXXXX|
            |                       |
            |        aktualny       |
            |                       |
            -------------------------
            |XXXXXXXXXXXXXXXXXXXXXXX|
```

Nic nie stoi na przeszkodzie, aby zacząć rysować wcześniej. 

Możemy zacząć rysować pierwszą linię w czasie wyświetlania ostatniej. 

Tym samym możemy przeznaczyć na rysowanie całą ramkę.

Czy można nie stosować dwubuforowania, gdy rysowanie trwa dłużej niż jedną ramkę? Oczywiście. 

Jest to wyjaśnione na rysunku 1c. Jeśli rozpoczniemy rysowanie po pobraniu przez ANTIC pierwszej linii (można użyć przerwania DLI), w pierwszej ramce zostanie wyświetlony stary obraz. Natomiast w drugiej ramce powinniśmy skończyć rysowanie, zanim ANTIC pobierze dane ostatniej linii. 

Wtedy zostanie wyświetlony cały aktualny obraz. Do pełnych dwóch ramek pozostaje jeszcze nieco czasu, oznaczonego jako "wolne".

Piotr Fusik (Fox/Taquart)


## Taquart Interlace Picture

Piotr Fusik (Fox/Taquart)


Artykuł ten opisuje tryb graficzny umożliwiający uzyskanie 256 kolorów w rozdzielczości 160x119.

### HIP

Niewątpliwie wielkim przełomem w wyświetlaniu grafiki na małym Atari było wynalezienie trybu HIP (Hard Interlace Picture). Tryb ten umożliwia wyświetlanie obrazów o dużej liczbie odcieni, w wysokiej (jak na komputer 8-bitowy) rozdzielczości 160x200, przy stosunkowo małym "migotaniu". Dokładne określenie ilości dostępnych odcieni jest kłopotliwe. Jest ona ograniczona z góry przez 30 (jasności od 0 do 14.5 co 0.5), jednak nie można swobodnie operować tymi 30 odcieniami, gdyż średnia ilość informacji o pojedynczym pikselu to 3.5 bitu (tryb 9 GTIA jest 4-bitowy, tryb 10 ma odcienie 3-bitowe).

Pomijając zamieszanie panujące wokół plików HIP (istnieją dwa różne formaty), uzyskanie tego trybu jest najprostsze przy ustawieniu rejestrów kolorów GTIA na wartości: $X0, $X2, $X4, $X6, $X8, $XA, $XC, $XE, $X0 (X jest cyfrą szestnastkową określającą kolor). Takie przyporządkowanie zajmuje wszystkie rejestry koloru (nie można np. wyświetlić kursora na duszku o innym kolorze), ale dzięki niemu co linię ekranową musimy zmieniać tylko tryb GTIA (na przemian 9 i 10).

### RIP

HIP posiada jedną podstawową wadę: jest monochromatyczny. Pomysłem na dodanie kolorów jest wypełnienie rejestrów kolorów GTIA kodami różnych kolorów.

Inny problem, również rozwiązany w formacie pliku RIP (Rocky Interlace Picture), to rozmiary obrazka, nie określone już "na sztywno". Co więcej, swobodę operowania kolorami możemy zwiększyć zmieniając wartości rejestrów kolorów GTIA w poszczególnych liniach.

Największą wadą RIP-a jest trudność operowania nim. Stworzenie programu graficznego, który umożliwiałby wygodne rysowanie w tym trybie jest trudnym zadaniem.

Problematyczna jest również konwersja - brak prostego kryterium wyboru kodów kolorów dla trybu 10 GTIA.

Trudności te są rekompensowane przez bardzo dobry wygląd odpowiednio przygotowanej grafiki.

### TIP

TIP jest rozszerzeniem HIP-a o kolory. Sposób dodania kolorów jest tak prosty, że dziwnym wydaje się, iż tryb ten nie powstał równocześnie z HIP-em.

Użyty został sposób kolorowania dotychczas stosowany dla trybów 256-kolorowych (APC, ILC), oraz do "zabarwiania" obrazów MIC (CIN). Kolory są nakładane przez linie trybu 11 GTIA. Linie te są wyświetlane w każdej ramce w tym samym miejscu, z tą samą zawartością. Linia kolorów jest zawsze nad odpowiadającą jej linią jasności.

Ponieważ, jak wiadomo, nie ma róży bez ognia, za kolory płacimy dwukrotnie mniejszą rozdzielczością pionową i wprowadzeniem ciemnych linii. Wygodne natomiast z punktu widzenia konwersji jest to, że piksele są kwadratowe.

Można rozważyć możliwość "interlace-owania" kolorów, tj. wyświetlania różnych kolorów w poszczególnych ramkach. Czy daje to dobry efekt, trzeba sprawdzić w praktyce.

___Wyświetlanie___

Sposób wyświetlania jest prostym rozszerzeniem wyświetlania HIP-a. Wartości rejestrów kolorów GTIA wynoszą $00, $02, $04, $06, $08, $0A, $0C, $0E, $00. Na pierwszym obrazie widzimy:

    pierwsza linia kolorów (GTIA 11)
    pierwsza linia jasności (GTIA 9)
    druga linia kolorów (GTIA 11)
    druga linia jasności (GTIA 10)...

natomiast na drugim:

    pierwsza linia kolorów (GTIA 11)
    pierwsza linia jasności (GTIA 10)
    druga linia kolorów (GTIA 11)
    druga linia jasności (GTIA 9)...

Jak widać, tryb TIP bez "mrugania" kolorami zajmuje mniej pamięci/dysku, niż HIP (ok. 12KB zamiast 16KB na obraz typowych rozmiarów).

___Konwersja___

Ponieważ nie powstały jeszcze żadne narzędzia umożliwiające bezpośrednio tworzenie grafiki w formacie TIP (więc na co czekasz, Fox - redakcja), ani nawet nie został określony format pliku TIP, najprostszą metodą uzyskania grafiki w tym trybie jest jej konwersja przy pomocy "większego" komputera a następnie napisanie procedury wyświetlającej.

Konwersję np. obrazu 24-bitowego można przeprowadzić następująco: należy zadbać o odpowiednią rozdzielczość i paletę.

W pierwszym przypadku wykonamy skalowanie/obcięcie, w drugim przekształcenie na paletę Atari (256-kolorową paletę kolorów Atari, w formacie Photoshop-a, można znaleźć np. w emulatorze Atari800).

Pozostaje w uzyskanym obrazku wyodrębnić kolory oraz "HIP-owe" dane dla trybów 9 i 10 GTIA. Najprostszym sposobem wydobycia kolorów jest wzięcie informacji o kolorze co drugiego piksela. Konwersja jasności na HIP może być problematyczna, ale prostym i dającym dobre efekty sposobem jest zapisanie jasności co drugiego piksela (począwszy od pierwszego) w trybie 9, a pozostałych w trybie 10. Jasności 9 GTIA kodujemy na 4 bitach, natomiast w trybie 10 ignorujemy najmłodszy bit jasności. Uzyskane w ten sposób dane dla trybów 11,9 i 10 możemy już łatwo wyświetlić.

Piotr Fusik (Fox/Taquart)




## Tryby graficzne 9++ oraz 10++

Piotr Fusik (Fox/Taquart)

Najczęściej używanym trybem jest chyba tzw. "tryb Konopa" użyty po raz pierwszy właśnie przez Konopa/Shadows w "Asskickerze". Od lat jest on wykorzystywany i nie pojawił się chyba żaden tryb będący równie "szybki" i dający podobne parametry ekranu (czyli proporcjonalne piksele, niedużą pamięć ekranu, 16 odcieni, ewentualnie inny tryb GTIA).

lewiS/AiDS "32 odcienie w trybie dziewiątym" (artykuł zamieszczony w "Atarynce" nr 1/2002)

W niniejszym artykule przedstawię sposób uzyskania trybu, który wizualnie różni się od "trybu Konopa" (znanego też jako tryb 9+) brakiem pustych linii i nazywa się, w zależności od użytego trybu GTIA, trybem 9++ lub 10++.

___Zalety nowego trybu___

- Tryb ten jest szybszy od trybu z pustymi liniami (9+).

- Display List jest znacznie krótszy (każda linia trybu jest tworzona przez jedną instrukcję DL).

- Dzięki temu, że DL dla tego trybu może ładować licznik pamięci obrazu tylko na początku, przy dwubuforowaniu nie jest wymagane tworzenie dwóch DL, a wystarczy zmienianie adresu obrazu zapisanego w DL.

- Można łatwo ustawić dowolną (do 16) wysokość linii trybu (np. 3,5 lub 6 zamiast 4).

- Wygląda to ładniej - jest to rzecz gustu, ale moim zdaniem kolory w trybie 10 GTIA wyglądają znacznie lepiej - tradycyjne czarne linie zmniejszają jasność i nasycenie.

___Wady___

- Tryb zapewnia mniejsze zużycie cykli przez ANTIC, kosztem dodatkowej pracy, jaką musi wykonać 6502. Operacji, które musi wykonać CPU, jest mało, niestety muszą one być odpowiednio zsynchronizowane z obrazem. W praktyce oznacza to, że uzyskanie zalety 1 nie jest takie proste, tj. wymaga pewnego nakładu pracy programistycznej.

- Jak wiadomo, istnieją problemy z wyświetleniem grafiki w ostatniej linii ekranu. Nie jest to przeszkodą dla trybu 9+, bowiem na końcu DL można umieścić rozkaz JVB, uzyskując 60 linii. W trybie 9++/10++ pozostaje nam zadowolić się 59 liniami lub... skorzystać z zalety 4 i zmniejszyć wysokość górnej lub dolnej linii do 3.

___Idea___

Pomysł jest prosty - sprawić, by ANTIC wyświetlał tę samą linię kilka razy, wykorzystując swoją wewnętrzną pamięć. Sytuacja taka ma miejsce np. w trybie 8 (systemowy GRAPHICS 3), gdzie dane są pobierane tylko w pierwszej linii, a potem już tylko z pamięci ANTICa.
Teoria

ANTIC posiada wewnętrzny 4-bitowy rejestr DCTR, który zlicza nr linii ekranowej. Normalnie dla każdej linii trybu zlicza on od zera do wartości zależnej od trybu (w interesującym nas przypadku trybu ANTICa 15 jest to 0). Sytuacja wygląda inaczej po włączeniu pionowego skrola. W pierwszej takiej linii DCTR liczy od VSCROL do 0, w następnych normalnie, a w ostatniej skrolowanej linii od 0 do VSCROL. "Liczy od a do b" należy rozumieć następująco: na początku do DCTR jest ładowana wartość a, pod koniec każdej linii DCTR jest porównywany w wartością b, jeśli jest równość, podejmowana jest decyzja o pobraniu kolejnej instrukcji Display List. W przeciwnym przypadku DCTR jest zwiększany o 1.

Załóżmy, że mamy następujący DL: $2F$0F oraz VSCROL=13 (dziesiętnie). Wtedy na ekranie widzimy:

    pierwszą linię 4 razy
    (wartości DCTR 13,14,15,0 - następuje "przekręcenie" z 15 na 0, gdyż DCTR jest 4-bitowy)
    drugą linię 14 razy (wartości DCTR od 0 do 13)

Natomiast dla VSCROL=3:

    pierwszą linię 14 razy
    drugą linię 4 razy

Co ważne, dane obrazu wyświetlane w kolejnych liniach ekranowych, są pobierane z pamięci tylko raz.

___Uzyskanie trybu___

Jak nietrudno się domyślić, żeby każda linia została wyświetlona 4 razy, tworzymy następujący Display List:

```
 b($6f),a(ekran)
 b($0f)
 b($2f),b($0f)...
```

i musimy tylko w odpowiednich momentach zmieniać zawartości rejestru VSCROL.

W zrozumieniu działania trybu powinien pomóc zamieszczony rysunek. 

Zostały na nim schematycznie przedstawione dwie linie trybu, czyli 8 linii ekranowych. 
Jest to zarazem zobrazowanie czasu (bez zachowania skali), który płynie wraz z wyświetlaniem każdej linii od lewej do prawej. 

Na początku rejestr VSCROL musi zawierać 13 (jest to rejestr 4-bitowy, więc górna połówka bajtu zapisywanego pod $D405 może być dowolna). 

Gdy ANTIC przepisze tę wartość do DCTR, gwarantuje to poprawne wyświetlanie pierwszej linii. 
Następnie będzie wyświetlana druga linia trybu i dopiero pod koniec jej ostatniej linii ekranowej wymagane jest, aby zawartość VSCROL wynosiła 3.

Mamy więc bardzo dużo czasu na wpisanie wartości 3 do VSCROL. Można to zrobić np. na przerwaniu DLI w pierwszej linii trybu. Gorzej jest z przygotowaniem do wyświetlenia kolejnej, tj. trzeciej linii trybu. Na rysunku został zaznaczony mały obszar, w którym powinniśmy wpisać 13 do VSCROL i rzeczywiście jest to niewielki przedział czasu.

```
            DCTR |                                                      |
           -----------------------------------------------------------------
VSCROL=13  * 13  |                                                      |
             14  |                                                      |
             15  | pierwsza linia trybu (bit 5 w rozkazie DL ustawiony) |
             0   |                                                      |
           -----------------------------------------------------------------
             0   |                                                      |
             1   |  druga linia trybu (bit 5 w rozkazie DL skasowany)   |
             2   |                                                      |
             3   | * tutaj startuje przerwanie DLI                      |   * VSCROL=3
           -----------------------------------------------------------------  VSCROL=13
                 |                                                      |
                  <----------------- widoczny obraz ------------------->
```

___Możliwe realizacje___

Aktualizację rejestru VSCROL, możemy wykonywać:

- a) używając przerwania DLI,
- b) wplatając ją w rozpętlony kod naszego efektu,
- c) używając jednego z przerwań liczników POKEY-a

Rozwiązanie **a)** jest niewątpliwie najprostsze w realizacji, niestety jest też najwolniejsze.

Optymalna jest realizacja **b)**, niestety można ją zastosować tylko w przypadku prostych efektów, jak np. bump mapping. 

Ciekawa jest realizacja **c)**, która ma tę przewagę nad **a** że przerwanie licznika POKEY-a można ustawić z dokładnością do cyklu, dzięki czemu nie musimy "wytracać" czasu po odebraniu przerwania. 
Niestety rozwiązanie to w praktyce (czyli w grze lub produkcji scenowej) odpada, gdyż liczniki POKEY-a służą jednocześnie do generowania dźwięku, a nie chcielibyśmy znacznie pogarszać muzyki (mniej kanałów) tylko dlatego, że chcemy włączyć ciekawy tryb graficzny.

___Procedura przerwania DLI___

Zależy nam na tym, aby obsługa tego przerwania zajmowała jak najmniej czasu. Okazuje się wystarczające użycie DLI co drugą linię trybu, tj. co 8 linii ekranowych, w rozkach DL ze skasowanym bitem 5. Przerwanie zostaje zgłoszone dość blisko początku ostatniej linii ekranowej linii trybu (patrz rysunek).

W ogólnym przypadku po odebraniu przerwania NMI należy sprawdzić jego rodzaj (DLI czy VBLKI) i zapamiętać rejestry (co najmniej akumulator). 
Mimo wszystko pozostaje dość dużo czasu, zanim powinniśmy wpisać 13 do VSCROL. 

Najprościej wytracić ten czas (i jednocześnie zapewnić właściwą synchronizację) korzystając z WSYNC. 
Następnie zapisujemy 13 do VSCROL i okazuje się, że jest już wystarczająco późno, aby wpisać tam 3. 

Jak widać na załączonym listingu, przerwanie jest też wywoływane przed pierwszą linią trybu, tj. w rozkazie tworzenia dwóch pustych linii. 
Zadając sobie dodatkowy trud, można zaoszczędzić nieco cykli wpisując zamiast tego 13 do VSCROL, np. na przerwaniu VBLANK i wywołując inną procedurę przerwania DLI w pierwszej linii trybu, która to procedura nie będzie musiała oczekiwać, a jedynie wpisze 3 do VSCROL.

To, co może nie być oczywiste na pierwszy rzut oka, to dlaczego w procedurze DLI wpisujemy 3 do VSCROL na końcu, zamiast np. przed zapisem do $D40A? 

Przecież na rysunku jest zaznaczone, że wartość VSCROL w drugiej linii trybu jest sprawdzana pod koniec linii ekranowej. 
Otóż istotnie właśniee tam następuje sprawdzenie, czy należy zakończyć wykonywanie aktualnego rozkazu DL.

Natomiast, jeśli jest wykorzystywane przerwanie DLI, musi ono być wywołane w ostatniej linii ekranowej linii trybu, dlatego występuje drugie (a pierwsze w kolejności wykonania) porównanie DCTR z VSCROL. Wobec tego VSCROL musi zawierać 3 już w momencie zgłaszania przerwania.
Ile cykli zyskujemy?

To pytanie jest ważne, bo przecież jako pierwsza zaleta tego trybu została wymieniona szybkość. Jedna linia trybu 9+ może zostać opisana w Display List następująco:

```
 b($0f),b($00)
 b($4f),a(ekran)
 b($00)
```

Razem: 6 cykli na DL + (64 lub 80) cykli na ekran (w zależności od szerokości). Dla trybu 9++ jest to jedna instrukcja DL, czyli 1 cykl na DL + (32 lub 40) cykli na ekran. Dodatkowo 6502 musi zaktualizować VSCROL, co trwa 6 cykli. Licząc cały ekran (instrukcja dwóch pustych lini, 59 linii trybu, w pierwszej linii trzeba podać adres ekranu - 2 cykle, rozkaz JVB) otrzymujemy:

    Wąski ekran:
    9+: 1+59*(6+64)+2+3=4136
    9++: 1+59*(1+32+6)+2+3=2307

    Normalny ekran:
    9+: 1+59*(6+80)+2+3=5080
    9++: 1+59*(1+40+6)+2+3=2779

Z grubsza zyskujemy więc ok. 6-7% czasu procesora. Niestety jest tak tylko w przypadku optymalnym, tj. wplataniu aktualizacji VSCROL w kod. 
Jeśli użyjemy przerwania DLI w przedstawionej postaci, okaże się, że tryb 9++ jest niestety nieco wolniejszy od trybu 9+ (ale wciąż wyraźnie szybszy od "tradycyjnego" trybu bez pustych linii). Jest tak ze względu na tracenie czasu w instrukcji "STA $D40A".

Dobrym (chociaż trudnym) rozwiązaniem jest wykorzystanie tego czasu np. na jakieś pożyteczne obliczenia. 
Nie należy też zapominać o innych zaletach trybu 9++, które mogą okazać się decydujące. 

Dodatkową zaletą jest to, że jeśli wykorzystujemy już przerwanie DLI, możemy niewielkim kosztem dokonać zmiany koloru tła w różnych miejscach ekranu.

Piotr Fusik (Fox/Taquart)

```
;	MODE 9++

	org $2000

	mwa #dli $200

	mva #$22 $22f
 
	mwa #dl $230

	mva #$40 $26f

	mva #$c0 $d40e

	jmp *


dli	pha
	sta $d40a
 
	lda #13
	sta $d405

	lda #3
	sta $d405

	pla
	rti

dl	dta $90,$6f,a($f000)	; 2 puste linie, 1 linia trybu
	:29 dta a($2f8f)	; $8f,$2f powtorzone 29 razy => 58 linii
  	dta $41,a(dl)
```

P.S. Opisaną metodę można zastosować do uzyskania innych ciekawych trybów, jak np. sprzętowy tryb tekstowy 40x40 znaków.

