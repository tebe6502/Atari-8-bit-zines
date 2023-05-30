#

## O formacie KOALI

<html>

<p>

Format zapisu KOALI MICROILUSTRATORA (PIC) jest obok MICropaintera, najpopularniejszym standardem zapisu grafiki na 8-bitowych komputerach Atari.
<br><br>
Dotychcasz ukazało się kilka artykułów na temat tegoż formatu zapisu (m.in. w MEGAZINIE i ABBUC MAG), jednak w pierwszym przypadku informacje te były niekompletne, zaś w drugim były pewne przekłamania i nieścisłości . Poza tym być może nie wszyscy mają te magazyny...

<br><br>
W tym artykule chciałbym opisać <b>POPRAWNĄ</b> budowę pliku KOALI, a w szczególności  jego nagłówka (jako że właśnie o nim były podane błędne informacje), opierając się na wiadomościach z dwóch powyższych Ľródeł oraz własnych spostrzeżeniach.

<br><br>
Format zapisu KOALI MICROILUSTRATORA powstał w 1983 roku w firmie Koala Ware. W tej lub lekko zmodyfikowanej wersji jest (był) także używany na innych komputerach, np. C64, Apple (!). Format ten rozpoznaje większość trybów graficznych oraz różne wielkości ekranu. Na Atari używa jednak (standardowo) tylko trybu gfx #15 z rozdzielczością ekranu 160x192 piksele.

<br><br>
Początek pliku w formacie KOALI to specjalny nagłówek, w którym zawarte są najważniejsze informacje o obrazku, tzn. jego szerokość, wysokość, kolory, itd.
W tym miejscu pozwolę sobie zaprezentować dokładny opis wszystkich bajtów nagłówka pliku PIC:

<pre>
<b>OFFSET=0</b> (4-bajty)
Nazwa: <b>Identyfikator formatu KOALI</b>
 Opis: Oznaczenie formatu Koali. Jest tu zawsze 255,128,201,199.

<b>OFFSET=4</b> (2-bajty)
Nazwa: <b>headln</b>
 Opis: Podaje długość nagłówka (tu miejsce jest w 2 bajtach), ale
       zwykle jest wartość=27, tzn. tyle bajtów ma nagłówek (27=$1b)
 
<b>OFFSET=6</b> (1-bajt)
Nazwa: <b>revision</b>
 Opis: Nr wersji programu względnie formatu obrazka.
       Normalnie jest to wartość=$01.
            
<b>OFFSET=7</b> (1-bajt)
Nazwa: <b>typcprs</b>
 Opis: Rodzaj kompresji:
                        0 = nieskompresowane
                        1 = kompresja pionowa
                        2 = kompresja pozioma
                        
<b>OFFSET=8</b> (1-bajt)
Nazwa: <b>antic-mode</b>
 Opis: Podaje tryb grafiki obrazka wg trybów ANTIC-a.

<b>OFFSET=9</b> (2-bajty)
Nazwa: <b>scrwidth</b>
 Opis: Szerokość obrazu w bajtach. Zwykle jest tutaj wartość = 40.

<b>OFFSET=11</b> (2-bajty)
Nazwa: <b>scrheight</b>
 Opis: Wysokość obrazu w bajtach. Zwykle jest tutaj wartość = 192.

<b>OFFSET=13</b> (5-bajtów)
Nazwa: <b>scrheight</b>
 Opis: Kolory obrazka - nagrywane w takiej kolejnośći jak w pamięci, 708..712.

<b>OFFSET=18</b> (2-bajty)
Nazwa: <b>picln</b>
 Opis: Ogólna długość (samego, bez nagłówka) obrazka w bajtach.

<b>OFFSET=20</b> (2-bajty)
Nazwa: <b>unused</b>
 Opis: Zawsze wynosi 0.
</pre>

<p>

To jeszcze nie wszystko o nagłówku... Od adresu <b>OFFSET+22</b> są 4 komórki zarezerwowane na tekst dla tytułu rysunku, autora i pozostałych uwag. Każda taka komórka tekstowa może mieć maksymalnie 40 znaków i musi być zakończona kodem <b>EOL</b> ($9b, #155 dec). Oczywiście żaden program nie używa tych komórek "tekstowych". Dlatego znaleĽć można tutaj normalnie wartość 155 powtórzoną cztery razy. Wpisując w to miejsce jakiś tekst trzeba go zakończyć EOL'em i zwiększyć odpowiednio długość nagłówka w komórce "headln" (tzn. podać nową wartość długości nagłówka, liczonej razem z "komentarzem").
<br><br>
<b>Nagłówek kończy</b> tzw. "spare byte" (zapasowy bajt). Wynosi on zazwyczaj 162 ($a2), chociaż popularny XL-Art, nagrywając w kompresji Koali wstawia tu wartość $a5.

<br><br>
Jest sporo do skomentowania odnośnie powyższej rozpiski nagłówka Koali.
Wg Bewesofta mogą być ładowane pliki z tylko częścią ekranu - ponoć oryginalny program KOALA M. potrafi je wczytać... Pozycja i rozmiar tzw. "okna", czyli części "scrwidth" i "scrheight". Te 4 bajty określają: początkową pozycję X (w bajtach, a nie w pikselach !), końcową pozycję X obrazu (pierwszą pozycją PO obrazku), początkową pozycję Y obrazu i końcową pozycję Y.

<br><br>
Kolory nagrywane są w kolejności takiej jak w pamięci (708-712), czyli w kolejne bajty od <b>OFFSET+13</b> jest nagrywanych pięć wartości. Wszystkie kolory można dowolnie ustawić w jakimś programie graficznym i ich wartości pojawią się w komórkach "colors" nagłówka KOALI. Jedynie może być problem z ustawieniem koloru inwersji ($2c7), który to można zmienić tylko w edytorach do logosowania grafiki... Ale to nieistotne, gdyż inwersja ważna jest tylko w grafice znakowej...

W każdym razie wartość, jaką można zwykle zastać (dla koloru rejestru $2c7) w nagłówku KOALI, to albo $00,  albo $46...

<br><br>
W użyciu może być <b>jeden z trzech typów kompresji</b> (7 bajt nagłówka) - wartość <b>$00</b> oznacza brak kompresji w obrazku, czyli, że reszta pliku (po nagłówku) zawiera tylko samą pamięć ekranu.

<br><br>
Wartość <b>$01</b> jest najczęściej używaną metodą. Oznacza ona spakowane dane, które zostaną umieszczone na ekranie w "pionowym" uporządkowaniu: najpierw bajty w liniach parzystych 0,2,4,6, itd. potem bajty w liniach nieparzystych 1,2,5,7 itd. Po rzędach "idą" w ten sam sposób kolumny ekranu.

<br><br>
Metoda <b>$02</b> również zawiera spakowane dane, ale będą one umieszczone na ekranie tak samo jak w metodzie $00 (poziomo).

<br><br>
Bajt 20-ty z nagłówka (nazwany "unused") został słusznie przeznaczony przez twórców formatu na przyszłe użycie. Pozwoliło to Hermesowi (autorowi viewera "ShowPIC v2.0") bardzo pożytecznie wykorzystać pierwszy bajt z pary "unused". Mianowicie został on użyty do przechowywania informacji dla GTIA o jej trzech dodatkowych trybach (tj. gfx #09, ,#10, #11). Pozwala to na wczytywanie skompresowanej grafiki również w w/w trybach graficznych, co oczywiście zaoszczędza miejsce na dysku... Oto jak zostało to zorganizowane...

<br><br>
Dwa najmłodsze bity pierwszego nieużywanego bajtu "unused" zawierają informację o powyższych trybach graficznych w następującej kolejności:
<pre>
    00 = zwykły tryb Antica (gfx #08)
    01 = 16 jasności tego samego koloru (gfx #09)
    10 = 9 dowolnych kolorów z palety 256 (gfx #10)
    11 = 16 kolorów o jednakowej jasności (gfx #11)
</pre>

<p>

Pozostałe bity z tego bajtu oraz drugi wolny bajt są przez viewer "ShowPIC v2.0" nieużywane. Powyższe wykorzystanie bajtu "unused" jest nazwane przez jego pomysłodawcę jako "PIC v2". Idea Hermesa jest zaiste genialna, lecz do tej pory spotkałem się z jej zastosowaniem tylko w "ShowPIC v2.0"... Warto byłoby ją upowszechnić...

<br><br>
Dużym problemem jest to, że większość tzw. Viewerów, Showerów, czy loaderów (programów odtwarzających format KOALI) potrafi ładować pliki PIC tylko ze standardową długością nagłówka, wynoszącą $1b (27) bajtów. Tymczasem, nagłówek może być teoretycznie zmienny, np. gdy dodasz jeszcze komentarz do obrazka od komórki <b>OFFSET+22</b> !!! Więcej, większość loaderów odczytuje z nagłówka tylko jedną rzecz - dane kolorów !!! Zauważył to już Bewesoft... Taki sposób działania tych programów można wytłumaczyć tylko jednym: LENISTWEM autorów tychże programików...

<br><br>
Jeśli zechcesz sobie np.dodać komentarz do rysunku, umieszczając go w nagłówku pliku, w odpowiednim miejscu, wiedz, iż na palcach można będzie policzyć programy, które to poprawnie odtworzą... Z przeprowadzonych przez mnie testów wynikło, że uda Ci się to tylko w:

<pre>
    - loaderze BeweSofta z ABBUC Magazine
    - ShowPIC v2.0 Hermesa
    - oryginalnym KOALA MICROILUSTRATOR
</pre>

<p>

(te trzy powyższe programy można ogólnie spokojnie uznać za najlepsze - dotąd - loadery dla formatu Koali)...

Z "eliminacji" odpadły natomiast loadery KOALI w takich programach, jak: GRAPH VIEW z CrisisSoft, GRAPH.COM Souseda, XL-Art,  RAMbrandt (!), BIT CONVERTER Bartmana oraz paru innych, o których akurat zapomniałem.

<br><br>
Problem "olewania" sobie wartości z nagłówka wynika również z innej, bardziej praktycznej (od wstawiania komentarzy do obrazków) rzeczy - przykładowo XL-Art przy zapisie PIC-a "zapomina" o zapisaniu w nagłówku Koali informacji o długości samego obrazka (nie wstawia nic do bajtów "picln" w nagłówku obrazka). 

<br>
Jako że większość "loaderów" również nie sprawdza bajtu "picln", wszystko jest OK... do czasu, aż napotkasz jakiś program, którego twórca spodziewał się, że są jeszcze dobrze napisane procedury obsługi kompresji KOALI i... w tymże programie nie zapomniał o tym bajcie... Wtedy zaczynają się kłopoty, bo program sprawdzający np. bajt "picln", po prostu (od razu) nie wczyta takiego PIC-a, który nie ma tam żadnej wartości (czyli "picln" = $00,$00). Po sprawdzeniu braku odpowiedniej wartości w nagłówku po prostu przerwie odczyt... Do tej pory spotkałem się z dwoma takimi przypadkami - w niezłym programie graficznym (dla trybu gfx #15) "Pixel Artist De Luxe v1.3" (swoją drogą jest on niezły dla posiadaczy tabliczki graficznej...) oraz w basicowym programie do wydruku obrazków "PICPRINT", zamieszczonym w jednym z wydań zinu "OHAUG"... Obydwa programy "buntowały się",  gdy chciałem wczytać jakiś PIC z XL-Art, ale przyczyna okazała się prozaiczna - brak tego jednego, jedynego bajtu, na który zwracały uwagę... Zatem aby do nich wczytać taki obrazek, należy wpisać do jego nagłówka odpowiednią wartość w bajtach "picln" za pomocą jakiegoś monitora (dyskowego)... Można też wczytać obrazek w postaci MIC do "Pixela..." i tam zgrać go jako PIC. Zostanie on zapisany w rzadziej spotykanej poziomej kompresji... Na szczęście nie będzie już kłopotów z ładowaniem tak "przerobionego" obrazka w drugą stronę, tzn. w np. XL-Art, bo on bajty "picln", jak już wcześniej wspominałem, ignoruje.

<br><br>
Wypadałoby na koniec podać jednak <b>budowę samej kompresji KOALI</b>... Oto,  jak to mniej więcej wygląda...

<br><br>
Same dane obrazka (tzw. mapa bitowa) są skompresowane prostym algorytmem RLE (redukcja powtarzających się elementów). Kiedy np. pięć razy, jeden za drugim wystąpi w obrazku wartość "0", nagrane zostaną jako "5x0". Obrazek jest umieszczony w poszczególnych blokach. Są dwa typy bloków użytych w kompresji KOALI:
<br><br>
<b>Dane niespakowane.</b> Pierwszy bajt (jako znacznik) ma ustawiony bit 7 (#128 dec), reszta tego samego bajtu stanowi długość bloku danych (maksymalnie 127 bajtów). Jeśli ta długość wynosi zero, to jest wtedy jeszcze o dwa bajty więcej - informują one o aktualnej długości (2-bajtowa wartość, więc będzie DOSYĆ długi niespakowany blok !). Następnymi bajtami są już same niespakowane dane.

<br><br>
<b>Dane spakowane</b>. Pierwszy bajt w takim bloku ma wyzerowany siódmy bit, reszta zaś jest długośćią bloku - tak samo, jak opisana wyżej. Tu jest tylko jeden bajt danych, który wypełni swą wartością wszystkie bajty w bloku. Po prostu informuje on o tym jaka wartość jest skompresowana, a ze znacznika (pierwszego bajtu w bloku, informującego o statusie i długości całego bloku) wynika, ile razy trzeba go powtórzyć. Tu także może wystąpić długi, spakowany (tym razem) blok składający się z 3 bajtów "informujących" i jednego bajtu danych - zasada jest podobna jak w bloku niespakowanym.

<br><br>
To byłoby na tyle w temacie budowy pliku w formacie KOALI MICROILUSTRATORA. Mimo, że efektywność kompresji w oferowany przez KOALĘ sposób jest raczej kiepska (szczególnie przy dużych skomplikowanych obrazkach), to zapis PIC jest bardzo popularny, zapewne głównie przez prostotę jego realizacji (format podobny do PIC stosuje np. edytor CIN, Trzmiel, RGB Shower, czy XL-Paint...). Jakby jednak na to nie patrzeć, (prawie) zawsze obrazek trochę się skróci i raczej w wyjątkowych przypadkach opłaca się trzymać plik MIC zamiast PIC-a.

<br><br>
Mam nadzieję, że zamieszczone tu informacje przydadzą się szczególnie koderom,  spośród których może ktoś wreszcie napisze przeglądanie obrazków w kilku(nastu) formatach graficznych (np. PIC, PIC v2, GED, CIN, DigiPaint, RGB, INT...).

<br>

<p class="tekst" align=right>
Specjalnie dla Was "produkował się"...<br>
-Dracon-
</p>

</html>
