#

## GED, czyli jak ulepszyć grafikę (1)

<html>

<div style="float: right">
<img src="../gfx/dracon.jpg" alt="dracon" width="80" height="117"><br>autor: dracon
<br>
</div>

<p>
 Wyobraź sobie, drogi Czytelniku,
program graficzny, umożliwiający uzyskanie w piętnastym trybie graficznym do 14
kolorów w jednej (!) linii ekranowej ...<br>
BEZ żadnego migania... Z możliwością zmiany
dziewięciu kolorów co każdą linię... Z pełną
możliwością zmian wszystkich komórek koloru trybu piętnastego oraz z (prawie) pełną
kontrolą nad wszystkimi obiektami PMG w
Atari (np. zmienianie, co każdą linię, ich koloru, szerokości, itd.)...
</p>

<p>
 A teraz... sprawdź, czy w Twojej kolekcji
programów przypadkiem nie pałęta się program "GED". To właśnie on jest edytorem
graficznym, który umożliwia wszystkie wyżej
wymienione przeze mnie operacje graficzne.<br><br>
GED'a z pewnością posiada wiele osób, jednak niewielu doceniło jego możliwości, a jeszcze mniej potrafi z niego korzystać.<br><br>
 Znam powód takiego stanu - mimo dość
dobrej, oryginalnej angielskiej instrukcji
do niego, sam program nie prezentuje się
ciekawie - pusty ekran, tylko na górze jest
mały prostokąt, oznaczający tryb pracy
GED'a. Duże potencjalne możliwości ulepszenia grafiki "piętnastki", jakie istnieją w
GED'zie, są niestety jakby "ukryte" przed
użytkownikiem z powodu jego nieciekawej
obsługi - mało funkcji, itp. sprawy.<br><br>
 Mam nadzieję, że po tym opisie GED'em
zainteresuje się więcej osób... Zapewniam,
że efekty pracy GED mogą być naprawdę
zadziwiające, a wszystko zależy od chęci
użytkownika oraz samego obrazka (jedne
obrazki można "podkolorować" na GED'zie
lepiej, inne gorzej... :)) ).<br><br>

 GED nie jest typowym programem graficznym. Jego autor stworzył go przede
wszystkim z myślą o uzyskaniu najlepszego
możliwego trybu graficznego bez migania,
jaki potrafi wyświetlić małe Atari. Ten tryb
wyświetlania zużywa prawie 10 kB kodu DLI
do zmiany rejestrów kolorów w każdej linii.
 Pozwala także umieszczczać obiekty PMG w
dowolnym miejscu na ekranie, dzięki czemu
uzyskuje się dodatkowe kolory.<br><br>

 GED i kod, który on zawiera, nie jest "public domain". Można go jednak rozpowszechniać bez żadnych opłat. Prawa autorskie należą do Johna Harrisa [ (c) 1993 by
John Harris ].<br><br>
 Autor programu prosi o skontaktowanie się
z nim w wypadku użycia formatu grafiki
GED'a w jakimkolwiek programie komercyjnym.
 Oczekuje też na wszelkie sugestie i pytania
na temat GED.<br><br>
 Oto jego adres:

<pre>
 John Harris
 45346 Graceway Dr.
 Ahwahnee, CA 93601, USA

Internet:
 jharris@cup.portal.com
</pre>

<p>
 Po tak upierdliwym wstępie czas na konkrety... :-)<br><br>

<p>
 <u>Podstawowa obsługa programu :</u>

<p>

<table width=100% cellspacing="1" cellpadding="1" border="1" frame="box" rules="all">
<tr>
	<td width=17%>*,+,-,=</td>
	<td>poruszanie kursorem</td>
</tr>
<tr>
	<td>joystick</td>
	<td>poruszanie kursorem</td>
</tr>
<tr>
	<td>Control *,+,-,=</td>
	<td>ruch co 8 pikseli</td>
</tr>
<tr>
	<td>Shift Ctrl -</td>
	<td>skok na górę ekranu</td>
</tr>
<tr>
	<td>0-3</td>
	<td>wybór aktualnego rejestru koloru (0=kolor tła)</td>
</tr>
<tr>
	<td>G</td>
	<td>pobiera kolor na pozycji kursora i ustawia na aktualny kolor<br>
	(tylko dla "normalnych" kolorów, tzn. nie  dotyczy to kolorów obiektów PMG)
	</td>
</tr>
<tr>
	<td>X</td>
	<td>wymienia dwa rejestry koloru. Aktualny kolor będzie wymieniony<br>
	na kolor na pozycji kursora
	</td>
</tr>
<tr>
	<td>Shift *,+,-,=</td>
	<td>zmienia kolor oraz jasność bieżącej "komórki koloru"</td>
</tr>
<tr>
	<td>C</td>
	<td>kopiuje pojedynczą "komórkę koloru"
 do następnej (niższej) linii obrazu.<br>
 Jeśli zmieniasz większą ilość linii, np. z góry na sam dół, to przytrzymaj ten <br>
 klawisz aby sobie ułatwić pracę</td>
</tr>
<tr>
	<td>W</td>
	<td>kopiuje całą linię "komórek koloru"
 do następnej linii obrazu</td>
</tr>
<tr>
	<td>, .</td>
	<td>przesuwają granice "komórki koloru"
 w lewo lub w prawo</td>
</tr>
<tr>
	<td>T</td>
	<td>wyświetla 'paletę testową' (widać
 tam np. gdzie są umieszczone duszki)</td>
</tr>
<tr>
	<td>SPACE</td>
	<td>przełącza tryb pracy GED'a :
 rysowanie lub wypełnianie</td>
</tr>
<tr>
	<td>U (undo)</td>
	<td>przywraca stan rysunku
 przed użyciem funkcji Fill
 (wypełniania)</td>
</tr>
<tr>
	<td>D</td>
	<td>przełącza tryb Fill'u: normalny (pełny)
 i 'dither' (kratka). Podaj liczbę 0-3,<br> co
 uformuje "kratkę" między tym wybranym,
 a aktywnym kolorem</td>
</tr>
<tr>
	<td>B</td>
	<td>przełącza tryb Brush'a (pędzla).
 Umożliwia powielanie fragmentu grafiki<br>
 (jednokolorowego) na ekranie.
 Kursor powinien być na obiekcie PMG,<br>
 który utworzy kształt pędzla</td>
</tr>
<tr>
	<td>P</td>
	<td>przełącza między trybem edycji
 'normalnych' kolorów (playfield),<br> a
 kolorami duszków (PMG)</td>
</tr>
</table>

<p>
Dalsze,
 poniższe funkcje można uruchomić
 po uaktywnieniu opcji "P" (włączenie
 części GED do obiektów PMG)
</p>
 <p>
 <table width=100% cellspacing="1" cellpadding="1" border="1" frame="box" rules="all">
<tr>
	<td width=17%>A</td>
	<td>włącza automatyczne wybieranie
 obiektu PMG pod kursorem</td>
</tr>
<tr>
	<td>1-4</td>
	<td>wybór duszka 1-4</td>
</tr>
<tr>
	<td>5-8</td>
	<td>wybór pocisku 1-4</td>
</tr>
<tr>
	<td>5-8</td>
	<td>wybór pocisku 1-4</td>
</tr>
<tr>
	<td>Shift 1-8</td>
	<td>zaznacza aktualną pozycję
 kursora jako poziomą początkową
 pozycję obiektu PMG</td>
</tr>
<tr>
	<td>&lt &gt</td>
	<td>zmienia bieżącą szerokość obiektu
 PMG : normalna/podwójna/poczwórna</td>
</tr>
<tr>
	<td>M</td>
	<td>przełącza bit pierszeństwa dla pocisków używanych jako 5-ty duszek</td>
</tr>
<tr>
	<td>O</td>
	<td>przełącza bit pierszeństwa (priorytet)
 dla nakładania kolorów PMG<br>(tzn. który
 duszek ma się pojawić nad /przed którym)</td>
</tr>
<tr>
	<td>F</td>
	<td>przełącza cztery tryby priorytetów
 playfield ("normalnych" kolorów) i PMG.<br>
 To zmienia który obiekt ukaże się przed
 innymi obiektami na ekranie,<br> "z przodu"
 (pierwszy tryb priorytetu GED'a to rysowanie
 na kolorze tła - kolor #0,<br> pozostałe
 zezwalają także na rysowanie duszkami
 na innych kolorach - #1, #2, #3...)</td>
</tr>
</table>

 <p>
 <table width=100% cellspacing="1" cellpadding="1" border="1" frame="box" rules="all">
<tr>
	<td width=17%>ESC</td>
	<td>a następnie numer 1-9 - pokazuje
 katalog dyskietki z wybranej stacji
 dysków.<br> Ta funkcja pozwala dodatkowo ustalić bieżącą (standardową) stację,<br> z której będą
odczytywane dane. Dzięki temu po odczycie
katalogu z np.<br> ramdysku (D8:) można przy
ładowaniu pliku pominąć nazwę urządzenia,<br>
a program przyjmie w tym przypadku, że tą
bieżącą stacją jest D8:<br> i wszystkie dane
będzie próbował ładować z D8:</td>
</tr>
<tr>
	<td>L</td>
	<td>ładowanie rysunku. Uwaga: nie musisz
 podawać nazwy urządzenia - program<br>
 odczyta wtedy dane ze stacji D1: lub
 (po zmianie, opisanej wyżej) z innej,<br>
 ustawionej jako standardowa, stacji</td>
</tr>
<tr>
	<td>S</td>
	<td>zapis rysunku. Jeśli już coś nagrywałeś,
 to pojawi się nazwa tego<br> ostatnio nagrywanego pliku wraz z urządzeniem
 (np. D1: PICTURE.GED),<br> teraz możesz
 potwierdzić tą nazwę, lub ją zmienić i
 zatwierdzić Return'em</td>
</tr>
<tr>
	<td>Shift X</td>
	<td>wyjście do DOS'u</td>
</tr>
<tr>
	<td>Shift Ctrl Tab </td>
	<td>czyści cały ekran</td>
</tr>
</table>


<p>
 <u>Rysowanie w GED :</u>
</p>
  <p>
 Do poruszania kursorem można używać
 joystick w porcie #1 lub strzałek kursora.
 Zamiast poruszania kursorem z klawiatury
co 1 piksel, można to zrobić z wciśniętym
klawiszem "Control -" ruch będzie co 8 pikseli.<br><br>
 Kombinacja "Shift Control -" (minus)
przeniesie kursor na samą górę ekranu.<br>
Jest to przydatne do zmiany rejestrów PMG.
Opiszę to przy okazji omawiania części GED
do obiektów PMG.<br><br>
 Fire' em w joysticku możesz rysować
używając aktywny (aktualny) kolor. Jeśli
na pozycji kursora był już piksel w tym samym kolorze co aktualny, to zostanie on
wymazany i będzie tam wstawiony kolor tła
(#0). Dzięki temu można prosto rysować i
kasować danym kolorem bez konieczności
wybierania koloru z klawiatury.<br><br>
 Klawiszami 0-3 wybierasz pożądany kolor
(rejestr koloru), kolor #0 oznacza tło.
Możesz też najechać kursorem na kolor na
obrazku, którym chciałbyś rysować i wcisnąć "G", by "pobrać" ten kolor.
 Kasowanie (czyszczenie) całego obrazu
następuje po wciśnięciu "Shift Control Tab".
 "Shift X" spowoduje wyjście do DOS'a.

<p>
 <u>Tryb wypełniania :</u>
</p>
 <p>
 Wciśnij SPACE aby wybrać między trybem
rysowania i wypełniania. U góry ekranu
znajduje się mała ikona informująca, który
 tryb aktualnie używasz. Jest ona linią w
trybie rysowania, natomiast podczas
wypełniania zmienia się w wypełniony prostokąt. Dodatkowym sygnałem używania
trybu wypełniania jest przyspieszone
miganie kursora.<br><br>
 Wypełnianie można uzyskać także w trybie
"kratki" (dither). Wciśnij klawisz "D", a
następnie numer 0-3. "Kratkowany" wzór
będzie uformowany między tym numerem a
aktywnym rejestrem koloru. Ikona pokaże
kratkowany prostokąt gdy opcja "kratkowania" będzie włączona.<br><br>
 Ponowne wciśnięcie "D" przywraca 'pełne'
wypełnianie.<br><br>
 Tryb wypełniania w GED to proste wypełnianie w dół, wewnątrz obszaru, gdzie ta
funkcja się rozpoczęła.<br><br>
 Wciśnięcie U (undo) cofnie skutki działania wypełniania.<br><br>
 Tryb Fill (wypełnianie) bieżąco wypełnia
tylko jeden rejestr koloru. Wszelkie zmiany
kolorów w linii nie są uwzględniane przy tej
 operacji, dlatego może być konieczne
"ręczne" kopiowanie tych zmian przy użyciu
komendy "C".<br><br>

 GED można podzielić na dwie części:
edycja standardowych kolorów (tzw. playfield) i edycja obiektów PMG (tzn. duszki
lub gracze oraz pociski).<br><br>
 W celu uzyskania dodatkowych kolorów w
obrazku można użyć jednego z tych dwóch
trybów lub też (co jest lepsze ale i bardziej skomplikowane) obu metod.<br><br>
 Zajmę się teraz częścią GED'a dotyczącą
kolorów "playfield". Na marginesie, w pierwszej wersji GED'a była tylko ta możliwość,
a dopiero później w kolejnej wersji autor
dodał 'obróbkę' PMG.


<p>
 <u>PLAYFIELD:</u>
</p>
 <p>
 Ponieważ rejestry kolorów są mnożone
wiele razy na jedną linię, zmiana w palecie
kolorów da efekt tylko w porcji (fragmencie) linii, który autor GED' a nazywa
"komórką koloru".<br><br>
 Aby zobaczyć, jak wygląda "komórka koloru", zrób następujący eksperyment:<br>
wyczyść ekran w GED ("Shift + Ctrl + Tab")
i wypełnij go pierwszym rejestrem koloru ("1", spacja i Fire).<br><br>
Wtedy porusz kursorem kilka linii w dół i
wypełnij go kolorem #2. Powtórz to samo z
kolorem #3. Teraz wciśnij "T" by włączyć
'paletę testową' i patrz na obraz. Rejestry
kolorów w danych "playfielda" nie były
zmieniane, lecz 'wielokrotne' kolory są "napchane" w nich, tworząc pionowe pasy koloru. Każda różna kolorowa część linii jest tą
tzw. "komórką koloru".<br><br>
 Na ekranie widać wyraźnie, że w jednej
linii jest kilka 'pasków' o różnym odcieniu,
różnie są one ułożone - raz jest to pół linii ekranowej, raz ćwierć i to właśnie jest
charakterystyczne dla "komórek koloru".<br><br>
"Komórkę koloru" można zdefiniować jako
rejestr koloru, który jest wyświetlany tylko dla CZĘ¦CI pojedyńczej linii obrazu.<br><br>
 Istnieje osiem "komórek koloru" na każdą jedną linię ekranową, ale musiałbyś rysować wszystkimi rejestrami koloru na tej
samej linii, ażeby zobaczyć wszystkie 8
"komórek koloru" w tej linii. Być może to
wszystko wydaje się skomplikowane, ale jak
zwykle potrzeba treningu aby to rozczaić...<br><br>

 Kolor tła (#0) nie jest zmieniany, lecz pozostałe trzy rejestry kolorów mogą być
wielokrotnie "faszerowane" różnymi wartościami. To stwarza te 8 kolorów "playfield"
w jednej, całej linii obrazu (tzw. scan line=
 linia skanowa).<br><br>
 Wartość rejestru koloru istnieje tylko dla
fragmentu linii skanowej i tworzy to, jak
już wyżej wspomniałem, "komórkę koloru".
W ten sposób ekran jest podzielony na
kolumny, tak jak pokazano niżej.<br><br>
 Działanie procedury DLI : linia skanowa
rozpoczyna się z początkowymi wartościami
 kolorów dla wszystkich trzech rejestrów
koloru. Następnie procedura DLI wstępnie
ładuje pierwsze zmiany trzech rejestrów
do rejestrów A, X i Y procesora. Zaczyna
się to faktycznie od 31-go piksela (poziomo,
bo wysokość nie jest akurat ważna), gdyż
tam jest ustawiana nowa wartość dla pierwszego
rejestru koloru.<br><br>


 (współrzędne dotyczą pozycji X kursora,
wartość Y [wysokość] nie jest tu ważna;<br>
Uwaga: położenie piksela trzeba liczyć od
pozycji 0)<br><br>

<pre>
- instrukcje DLI -
                                       LDA#      LDA#
        STA        STX       STY       STA       STA
       $D016      $D017     $D018     $D016     $D017
         |          |         |         |         |
X:      31         63        83        107       131
pierwszy | nowy     |  drugi  |  drugi  | 3.      | 3.
zestaw   | (drugi)  |  kolor  |  kolor  | wart.   | wart.
kolorów  | kolor #1 |  1-2,   |  #1-#3  | dla     | 1-2
#0-#3    | i oryg.  |         |         | kol. #1 | 2.
istnieje | #2-#3    |  oryg.  |         | 2.      | wart.
tutaj    | kolory   |  #3     |         | wart.   | dla
         |          |         |         | dla 2-3 | #3
</pre>
<p>
 
 To jest rozkład dla przerwania DLI, lecz
wzrokowo, ważniejsze jest, aby widzieć
gdzie są "komórki koloru", ponieważ to
jest to, z czym rysujesz.<br><br>

<pre>
"komórki koloru":
 
0         31             107
Pierwsza  | Druga wartość | Trzecia
wartość   | koloru #1     | wartość
koloru #1 |               | koloru #1

0         63             131
Pierwsza  | Druga wartość | Trzecia
wartość   | koloru #2     | wartość
koloru #2 |               | kol. #2

0         83
Pierwsza  | Druga
wartość   | wartość
koloru #3 | koloru #3
</pre>
<p>

Nie ma żadnej trzeciej wartości dla koloru
 #3 (dla $D018). Spowodowane jest to tym,
że nie starcza już czasu na jego zmianę.<br><br>


 Pozycje piksela na powyższym planie są dla
standardowego ustawienia. GED pozwala
również na przesuwanie całej "procedury"
 (tzn. granicy "komórek koloru") w lewo lub
w prawo, za pomocą klawiszy "," i "."<br>
 - dobrze widać to po włączeniu 'palety testowej' (klawiszem "T").<br><br>
 Oczywiście wszelkie zmiany w lewo lub w prawo będą zmieniać wszystkie współrzędne
pikseli z powyższej tabeli.<br><br>

 Myślę, że teraz już wiesz na czym polegają "komórki koloru". Oznaczają one, że
zależnie od położenia kursora (na której
jest on linii), zmienianie wartości rejestru
koloru (z użyciem "Shift strzałek") zmienia
TYLKO lokalną (miejscową) "komórkę koloru"
Zmieni się kolor w części linii. Kolory "playfield" są "upychane "automatycznie w każdej
linii i takie zmienianie "komórki koloru" działa tylko w tej linii skanowej, która jest
zmieniana.<br><br>
 Do zmiany kolorów używaj : "Shift +,*"
zmieni kolor, a "Shift -, =" jasność tego
koloru.<br><br>
 Zmiana koloru obrazu daje efekt tylko w
jednej linii, dlatego autor dołożył dodatkowe funkcje: wciśnięcie "C" skopiuje bieżącą "komórkę koloru" do tej samej, o 1 linię niższej komórki. Możesz trzymać "C"
aby powtarzać tą operację. Używaj funkcji
 "C" gdy zmieniłeś właśnie jeden kolor i nie
chcesz zmieniać pozostałych "komórek koloru".<br><br>
 Z kolei klawisz "W" skopiuje całą linię "komórek koloru" do następnej linii na dole.
Użyj tej funkcji, gdy zmieniłeś wszystkie
rejestry koloru (#1,#2,#3) i chcesz skopiować całą paletę.<br><br>

 Komenda "X" pozwala na wymianę dwóch rejestrów koloru obrazu. Jeden rejestr powinien być wybrany z klawiatury: 0-3 (lub
przez komendę "G"). Wtedy umieść kursor
na 'szczycie' koloru, który chcesz zmienić i
 i wciśnij "X". Komenda ta zadziała wszędzie
poniżej aktualnej pozycji kursora na ekranie oraz na prawo od pozycji kursora.
Wymieniony będzie także aktywny rejestr
koloru. Ponieważ punkt na pozycji kursora
był wymieniany, mając aktywny kolor możesz
wcisnąć "X" drugi raz aby przywrócić stan
sprzed zamiany.<br><br>

<p>
 <u>Granice komórek koloru</u>
</p>
 <p>
 GED pozwala na przemieszczenie położenia
granic "komórek koloru" w lewo lub w prawo
jako grupy. Normalnie jest to pierwszy
krok, aby podczas kolorowania obrazka
osiągnąć najlepsze dopasowanie granic
"komórek koloru" do obiektów na obrazku.<br><br>
 Jest to zmienianie granic na całym obrazie i
nie może być zmieniane w połowie ekranu.
 Jak już wyżej wspomniałem, do przesuwania
granic "komórek" należy użyć "," i "." .<br>
 Komenda "T" zmienia obraz na 'paletę testową', co powoduje łatwiejsze zobaczenie
granic między "komórkami koloru". Ponowne
wciśnięcie "T" przywraca normalną paletę
obrazu.

<p>
 <u>KOLOROWANIE</u>
</p>
 <p>
 Kolorowanie obrazka trzeba przeprowadzić
etapami. Po załadowaniu grafiki trzeba ją
najpierw podkolorować "globalnie", czyli
ustawić jakie kolory mają być jako podstawowe na całym ekranie. Jest to konieczne, bo GED ignoruje informację o kolorach z pliku .MIC i zawsze po wgraniu
obrazka ustawia kolor szary.<br>
 Najlepiej zacząć kolorować od prawej górnej strony rysunku (użyj kombinację
 Shift & Ctrl & - aby przenieść kursor na
pierwszą górną linię ekranu lub ustaw tam
kursor joystickiem). Ustawiłeś już kursor
w prawym górnym rogu ekranu ??? OK,
teraz najedź na piksel z danym rejestrem
koloru (którymś z trzech podstawowych
 rejestrów trybu gfx #15 OS : #0=$2C8, #1=$2C4, #2=$2C5, #3 =$2C6)


 i kombinacją "Shift strzałki" ustaw jego
pożądany kolor i jasność. Następnie ustaw
kolor i jasność pozostałych rejestrów koloru w tej linii. Używając funkcji "W" i "C"
przekopiuj już odpowiednio ustawione kolory na wszystkie dolne linie, aż do samego
dołu obrazu. Po tym przenieś kursor znowu na sam szczyt obrazu, tyle, że ustaw go
na "komórce koloru" obok właśnie zmienionej (czyli z prawej strony, ale już bliżej
środka ekranu). Powtórz numer z ustawieniem odpowiedniego koloru dla wszystkich
trzech rejestrów koloru i skopiuj to aż na
sam dół ekranu, wtedy znów zacznij od samej góry ekranu na kolejnej "komórce
koloru" itd. aż dojdziesz do dolnego lewego
rogu ekranu, czyli będziesz mieć podkolorowany (wstępnie) cały rysunek. Dopiero
 teraz możesz dokonać poszczególnych
zmian kolorów, np. na środku ekranu lub
nałożyć duszki , itd.<br><br>

 Kolorowanie w GED jest dosyć denerwujące,
gdyż często się zdarza, że zmieniając kolor
aktualnej "komórki koloru" np. na środku
ekranu (przede wszystkim z użyciem funkcji "W"), zmienia się także niepotrzebnie
już ustawiony rejestr koloru w sąsiedniej
"komórce koloru" w tej samej linii obrazu
 (np. z prawej strony).<br><br>
 Dlatego podczas kolorowania należy na to
uważać. Jeśli coś takiego wystąpi, to potrzeba nieraz kilkukrotnych poprawek,
używania zamiennie funkcji "W" i "C". Wymagana jest cierpliwość, bo możliwe jest uzyskanie pożądanego koloru na całym ekranie, trzeba "tylko" trochę pokombinować !<br><br>

<p>
 <u>Format zapisu w GED</u>
</p>
  <p>
  
 GED nagrywa jeden duży plik binarny
(dosowy - z nagłówkiem $FFFF) o długości
 11302 bajty (licząc z nagłówkiem), o
 adresie $5330-$7F4F.<br><br>
 Plik taki zawiera wszystkie potrzebne programowi dane, a więc sam obrazek, ustawienie palety kolorów dla niego oraz dane
obiektów PMG.<br><br>
 Obrazek w GED zajmuje dużo miejsca na
dysku (45 sektorów w podwójnej gęstości)
ponieważ autor nie zastosował w obecnej
wersji GED żadnej metody kompresji pliku.
Zapowiada jednak zrobić to w kolejnych,
przyszłych wersjach tego programu.<br><br>

Oto rozkład dla poszczególnych elementów
GED'a, które są w pamięci (i zapisanym
przez GED pliku) podczas edycji rysunku:

<pre>
 $5330-$5AFF - dane palety koloru
 $5B00-$5FFF - dane obiektów PMG
 $6000-$600F - nagłówek obrazka
 $6010-$7F4F - dane obrazu

 (dla rozdzielczości 160x200)
</pre>
 <p>
 Teraz czas na...
</p>
 <p>
 <u>Informacje dodatkowe</u>
 <p>
GED pracuje w piętnastym trybie graficznym
OS (czyli w trybie #$0E Antica) w rozdzielczości 160x200 pikseli. Jako że wszystkie
inne programy graficzne dla trybu #15.
używają rozdzielczości 160x192, GED oferuje dodatkowe osiem linii ekranowych.
Można to olać, zostawiając po prostu wolne
miejsce, albo też dorysować coś do rysunku w tych wolnych ośmiu liniach (po wcześniejszym wgraniu jakiejś /swojej/ grafiki
w standardowej rozdzielczości 160x192),
lub też, ewentualnie, narysować te osiem linii
na swoim ulubionym programie graficznym
 ("XL- ART" ??), następnie dodać do tego
nagłówek binarny : $7E10-$7F4F i taki plik
wgrać podczas pracy w GED'zie komendą "L".<br><br>
 Tu ujawnia się wielka, moim zdaniem, zaleta
GED'a - pozwala on ładować pliki binarne z
różnymi danymi. Możliwe jest to podczas
działania programu, za pomocą wyżej wymienionej komendy. Dzięki temu można
ładować różne "palety koloru", czy też
obiekty PMG w trakcie edycji jednego obrazka (w celu np. dobrania odpowiedniego
ustawienia kolorów spośród kilku 'palet'
nagranych na dysku), a program sam
umieści dane w odpowienim miejscu pamięci
(o ile w nagłóweku był dobry adres). Takie posunięcie autora zlikwidowało konieczność istnienia specjalnych, oddzielnych
funkcji LOAD i SAVE dla obrazka, PMG itd.<br><br>

 Bardzo ważne są dwie sprawy:<br><br>

1. Dane dla GED'a muszą mieć odpowiednie
adresy, np. dane kolorów powinny mieć nagłówek binarny $5330-$5AFF. Adresy poszczególnych danych do ładowania znajdują
się powyżej (patrz : "Format zapisu w GED").
Ogólnie nie radzę ładować do GED czegoś,
 co nie ma nagłówka dosowego z przedziału
adresów $5330-$7F4F.<br><br>

 2. Próba załadowania funkcją "L" jakiegoś
pliku, który w ogóle nie ma nagłówka binarnego (dosowego) na ogół zawiesi program,
tak więc z góry to odradzam.<br><br>

 Aktualna, posiadana przeze mnie wersja
 GED (v2) nie ma możliwości nagrywania poszczególnych danych (danych PMG, palety
kolorów, danych samego obrazka) jako pojedynczych plików binarnych (w celu późniejszego ładowania ich do GED'a, jak to
opisałem wyżej). Możliwe jest to dopiero
po wyjściu z tego programu (kombinacją
"Shift X"), w DOS. Funkcja "SAV" lub "K",
w zależności od używanego DOS'a (ja używam najczęściej DOS II+/D, więc do zapisu
danych wykorzystam polecenie "SAV")
umożliwi zgranie na dysk wybranego elementu z GED. Np. w moim ulubionym DOS
II+/D w celu nagrania 'PMG' na dysk
wykonam komendę :
<pre>
 "SAV PMG . OBJ, 5B00, 5FFF"
</pre>
 <p>
Pozostał jeszcze jeden problem, mianowicie:

<p>
 <u>Import grafiki</u>
</p>

 <p>

 Jakkolwiek nic nie stoi na przeszkodzie aby
od początku do końca narysować swoje
arcydzieło pod samym GED'em, myślę jednak,
że jest to zajęcie dla ludzi cierpiących na
nadmiar czasu i cierpliwości... :)<br><br>
Znacznie lepszym pomysłem jest wykorzystanie już narysowanego obrazka (na
innym programie graficznym, ze względu na
dostępność wielu "narzędzi malarskich") i
 następnie załadowanie go do GED'a celem
podkolorowania.<br><br>
Istnieją dwie metody przeniesienia rysunku
Pierwsza, to dodanie do obrazka nagłówka
binarnego (dosowego) o adresie zaczynającym się od $6010. Standardowy plik .MIC
ma długość 7684 bajty (7680 bajtów samych danych obrazu plus cztery bajty
informujące o kolorach obrazka). Zatem
jego nagłówek będzie następujący :<br>
 $6010-$7E13.<br><br> Tu mała uwaga: właściwe
dane są od $6010 - $7E0F, reszta (4 bajty)
to zbędne (dla GED) info o kolorze. Teraz
można już wczytać do GED swój obrazek,
ale należy pamiętać o tym, że po wczytaniu,
na samym dole ekranu pojawią się dodatkowe, małe "śmieci" (pozostałość z danych
kolorów w pliku .MIC, które GED zinterpretował jako dalsze dane dla obrazka).
Musisz to wymazać, rysując kolorem #0
 (tła).<br><br>
 Możliwa jest też jeszcze dodatkowa trudność - po wgraniu może pojawić się dziwne
ustawienie jasności na obrazku, jeśli dany
obrazek nie ma "ustawień jasności" wg
standardu XL-ART 'a :<br>

#0=$x0 #1=$x4, #2=$x8, #3=$xC
rej. kol. rej.kol. rej.kol. rej.kol.
<br>
 (x, czyli dane o kolorze, GED ignoruje i
wstawia tu zawsze kolor szary).<br><br>

 Aby sobie z tym poradzić, trzeba albo
użyć programu Bartmana - "Bit converer"
(do zamiany kodów kolorów na odpowiadające powyższemu ustawieniu), albo po prostu
spojrzeć kilka (dziesiąt) linijek wyżej na
punkt pt. "KOLOROWANIE" i ustalić pożądane
jasność i kolor, zaczynając od samej góry
ekranu w GED.<br><br>
OK, po tych zabiegach można jeszcze ewentualnie dograć z dysku dodatkowe osiem
linii obrazu (powinny one mieć nagłówek :
 $7E10-$7F4F,
 tak, jak to wcześniej opisywałem ; pomijając 6-bajtowy nagłówek, te 8 linii ma długość 320 bajtów).<br><br>

 Drugą, zdecydowanie bardziej polecaną
przeze mnie metodą 'importu' obrazka jest
użycie programu "MICGED", autorstwa Peta
z Bit Busters.<br><br>
 "MICGED" konwertuje pliki .MIC na format
pliku .GED. Program ten jest bardzo wygodny użyciu, nie wymaga żadnego kombinowania poza wgraniem normalnego pliku .MIC
(nawet z niestandardowym ustawieniem
jasności rysunku) i nagraniem gotowego
obrazka w formacie GED'a, który można
wczytać funkcją "L" tego ostatniego.
 Konwerter ten "obcina" również zbędne
bajty z końca pliku .MIC. Przekonwertowany
w ten sposób obrazek można dalej "obrabiać" w GED, dodając mu odpowiednie kolory,
 itd.<br><br>

 OK, myślę, że jak na pierwszy raz, tyle
informacji o GED wystarczy...<br><br>

 Następnym razem napiszę co nieco o wykorzystaniu obiektów PMG w tym programie, o
pewnych problemach z tym związanych oraz
o używaniu "pędzli" (z ang. "brushes") . . .
Przewiduję też jakiś bonus dla (przyszłych ???) użytkowników GED, w postaci dodatkowych danych dla tego edytora... :)<br><br>

 Tym razem, jako uzupełnienie tego artykułu pozwoliłem sobie dodać zarchiwizowany
plik "GEDSTUFF.ARC"... ARChiwum to zawiera
główny przedmiot niniejszego tekstu, czyli
sam program - GED v2. Jest tam też "ściągawka" z funkcji do niego, konwerter "MIC-GED", parę przykładowych obrazków i....
ale to już trzeba sprawdzić samemu... :))
Do rozkompresowania tego pliku należy
użyć programu "Super UnArc v2.4"... Jak
to zrobić było dobrze opisane w "BARYMAGU
 #1", ale powinno być też gdzieś w "ENERGY".<br><br>

 Podsumowując moją opowieść o GED: jeśli
zajmujesz się tworzeniem grafiki na Atari
XL/XE, potrzebujesz dużo kolorów w swoich
obrazkach i nie lubisz tzw. trybu 'interlace',
to zostaje Ci GED, który, moim zdaniem,
pozwala uzyskać dużą ilość kolorów "naraz" na ekranie, dzięki użyciu DLI i PMG.
 Po prostu: GED albo interlace - wybór
należy do Ciebie...<br><br>
 Do zobaczenia (przeczytania) w kolejnym
odcinku o GED...<br><br>


 Specjalnie dla magazynu >> ENERGY <<
 opis do GED przygotował
 Dracon/USG/TQA

</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>
</p>

</html>

<hr>


## GED, czyli jak ulepszyć grafikę (2)

<html>

<div style="float: right">
<img src="../gfx/dracon.jpg" alt="dracon" width="80" height="117"><br>autor: dracon
<br>
</div>

<p>
                    <p>Serdecznie witam wszystkich zainteresowanych tytułowym edytorem graficznym i zapraszam na dokończenie jego szczegółowego opisu. Tak więc niniejszym ogłaszam ciąg dalszy tra-GED-ii... ;-)))</p>
                    <br>
                    <p>W poprzednim odcinku opisałem wszystkie polecenia GED oraz podałem szczegółowy sposób postępowania w jednym z dwóch trybów pracy tego programu, to jest w trybie "playfield". Ten tryb edycji, oferujący możliwość kilkukrotnego zmieniania  3 rejestrów koloru w jednej linii ekranowej (niektórzy określają to mianem tzw. "ścigania plamki" ), jest już zdecydowanym krokiem naprzód w porównaniu z innymi, starszymi rozwiązaniami. Mam tu na myśli RAMbrandta, Color Enhancer, Colors i parę inych, które używając przerwania DLI umożliwiały co prawda uzyskanie na obrazku do 128 kolorów, ale w jednej linii mogły być naraz tylko 4 różne kolory. Nie twierdzę, że nie można mimo wszystko tworzyć tam wspaniałych, wielokolorowych grafik (dowodem na to są bardzo ładne obrazki Ravena/Quasimodos w demie "Drunk Tank", gdzie po mistrzowsku zostały wykorzystane możliwości standardowego przerwania DLI), ale naprawdę są duże ograniczenia dla grafika chcącego wielu kolorów w różnych miejscach ekranu. Możliwości GED w trybie "playfield" są już nieco lepsze, choć "nigdy nie jest tak dobrze, żeby nie mogło być lepiej"... Myślę, że dodanie przez autora edycji i użycia PMG znakomicie dopełniło tryb "playfielda" i rzeczywiście J. Harrisowi udało się uzyskać najlepszy możliwy tryb graficzny bez żadnego migania, jaki potrafi wyświetlić Atari XL/XE. Zresztą pojawił się już nowszy edytor graficzny - "POWER GRAPHICS", który wykorzystuje właściwie identyczne założenia, tyle, że może on pracować w kilku trybach graficznych ( nie tylko w trybie gfx #15, jak GED ).</p>
                    <br>
                    <p>
                        <strong>Małe info...</strong>
                    </p>
                    <p></p>
                    <p>GED ma pełną kontrolę nad wszystkimi rejestrami grafiki PMG, lecz w znacznie bardziej ograniczonym zakresie, w porównaniu z edycją standardowych ("playfield") kolorów.</p>
                    <br>
                    <p>Warto byłoby najpierw przypomnieć sobie podstawowe wiadomości o grafice PMG, gdyż będzie to przydatne podczas używania GED'a...</p>
                    <br>
                    <p>Duszek ( sprajt, z ang. sprite ) jest definiowanym przez użytkownika obiektem, który można umieszczać w dowolnym miejscu ekranu i płynnie przesuwać (oraz animować). W Atari możliwe jest uzyskanie dwóch rodzajów duszków: większych - graczy i mniejszych nazwanych pociskami. Dlatego noszą one oficjalną nazwę grafiki graczy i pocisków (Player/Missile Graphics, w skrócie PMG). Duszków jest osiem: czterech graczy i cztery pociski. Tworzone są one przez układ GTIA, który "miesza" je z normalnymi danymi ( z "playfield" ) wyświetlanego obrazu. Dzięki temu duszki są niezależne od pozostałych parametrów obrazu i mogą być używane we wszystkich trybach graficznych (szczególnie nadają się, moim zdaniem, do trybu piętnastego OS, ze względu na to, iż mają takie same piksele w standardowej ich rozdzielczości). Duszki są połączone parami gracz-pocisk i ponumerowane od 0 do 3 (uwaga: w GED, dla wygody używania, autor zmienił numerację i jest to  1-4 ! )... Liczbę duszków można zwiększyć przez zastosowanie DLI, lecz akurat nie ma tej możliwości w GED...</p>
                    <br>
                    <p>
                        <strong>Wyróżnić można następujące cechy duszków:</strong>
                    </p>
                    <p></p>
                    <p>- szerokość gracza 8 punktów (pikseli), a pocisku 2 punkty (piskelki takie jak w trybie gfx #15 OS);</p>
                    <br>
                    <p>- dowolna wysokość wszystkich duszków</p>
                    <br>
                    <p>- możliwość dwukrotnego lub czterokrotnego zwiększenia szerokości (dwukrotna - piksele duszka takie jak piksele w trybie gfx #9 OS, czterokrotna - cztery razy 'grubsze' piksle duszka w porównaniu z standardowa szerokością; Jeśliby na maxa rozszerzyć wszystkie obiekty PMG, to można nimi zasłonić cały ekran... co możę być szczególnie przydatne, tu - w programie GED, ale o tym później...)</p>
                    <br>
                    <p>- jedno - albo dwuliniowa rozdzielczość pionowa (chodzi tu o wysokość każdego punktu duszka - jednoliniowa to wysokość piksla taka jak w "piętnastce", a dwuliniowa to rozdzielczość pionowa "siódemki");</p>
                    <br>
                    <p>- kolor ustalany oddzielnie dla każdej pary gracz-pocisk;</p>
                    <br>
                    <p>- możliwość tworzenia duszków wielokolorowych (poprzez ich nakładanie na siebie i operację ORA);</p>
                    <br>
                    <p>- ustalony priorytet wyświetlania między duszkami (który na/za którym ma się pokazać);</p>
                    <br>
                    <p>- wybierany priorytet wyświetlania duszków i tła (czyli co się ma pojawić "na wierzchu");</p>
                    <br>
                    <p>- możliwość łączenia pocisków w piątego gracza (mającego niezależny od pozostałych graczy kolor);</p>
                    <br>
                    <p>- wykrywanie kolizji pomiędzy duszkami (szczególnie użyteczne w grach...);</p>
                    <br>
                    <p>- wykrywanie kolizji duszków z tłem (uwaga jak wyżej...);</p>
                    <br>
                    <p>Ufff... Trochę tego było, ale to chyba wszystko, co trzeba wiedzieć o PMG przy używaniu GED - resztę doczytacie sobie podczas dalszej części tego wykładu...</p>
                    <br>
                    <p>Chyba za daleko odszedłem od głównego tematu... :-)) ... Pora zatem przedstawić jak wygląda w GED...</p>
                    <br>
                    <p>
                        <strong>Edycja PMG:</strong>
                    </p>
                    <p></p>
                    <p>Przechodzimy do niej po naciśnięciu klawisza "P" (przełącza on między edycją PMG a "playfield"). Po przejściu do trybu PMG obok ikonki Draw/Fill pojawi się (z lewej) drugi mały prostokąt - symbol auto-wybierania dowolnego obiektu PMG, który jest poniżej bieżącej pozycji kursora. Możesz teraz wprowadzić komendy dla PMG, które automatycznie użyją obiektu PMG na pozycji kursora, jeśli takowy tam istnieje (tzn. jest tam umieszczony). Nic się nie stanie (nie zadziała), jeżeli PMG na tamtej pozycji nie będzie.</p>
                    <br>
                    <p>Poszczególne obiekty PMG mogą być wybierane ręcznie (osobno) przez wciśnięcie klawiszy 1-4, aby wybrać graczy 1-4, albo 5-8, by wybrać pociski 1-4. Ręczna selekcja może stać się konieczna, jeśli dwa obiekty PMG nachodzą na siebie, bo procedura auto-wybierania zawsze wybierze niższy numer (obiekt) PMG. W razie czego, zawsze można powrócić do auto-selekcji PMG klawiszem "A" (który ją włącza i wyłącza).</p>
                    <br>
                    <p>Teraz podam uproszczony (aczkolwiek skuteczny !) sposób tworzenia obiektów PMG w GED:</p>
                    <br>
                    <p>1. Wciśnij "P" (włączenie edycji PMG);</p>
                    <br>
                    <p>2. Klawiszem "F" ustaw pożądany priorytet PMG (oznacza to, na którym kolorze mają się pojawić duszki, najlepiej jednak tego nie zmieniać, wtedy duszki będą widoczne na kolorze tła - #0. Dlaczego nie zmieniać ?! O tym na koniec opisu... );</p>
                    <br>
                    <p>3. Ewentualnie przełącz klawiszem "O" priorytet między samymi obiektami PMG (tzn. jak mają się między sobą "zachowywać" duszki... Jednak na początek lepiej niczego tutaj nie zmieniaj... );</p>
                    <br>
                    <p>4. Wybierz konkretny obiekt PMG, naciskając odpowiednią dlań cyfrę (1-4 = duszki, 5-8 = pociski). Zauważysz u góry kilka kropek (ilość ich zależna jest od nr wybranego obiektu PMG, np. cztery, to czwarty gracz lub pocisk... );</p>
                    <br>
                    <p>5. Ustaw kursor tam, gdzie ma być 'początek' (góra) duszka na ekranie i wciśnij Shift + nr obiektu PMG, który wybrałeś (np. Shift + 4);</p>
                    <br>
                    <p>6. Teraz postaw parę piksli na ekranie "w ciemno" (Fire'm), na prawo i poniżej pozycji kursora, gdzie ustawiłeś początek obiektu PMG. Duszka jeszcze nie widać, ale wciśnij kilkukrotnie Shift + "-" (strzałka w górę) - duszek wyłoni się z obłoków ciemności ekranowej i łaskawie pozwoli Ci przeprowadzać dalsze operacje na nim... :-)</p>
                    <br>
                    <p>7. Widząc duszka, możesz już spokojnie i dokładnie utworzyć go w/g pożądanego kształtu... Użyj przycisku Fire, aby kasować/dodawać piksele tworzące obiekt PMG. Pamiętaj, że na razie maksymalna szerokość PMG, z jaką możesz narysować duszka, to 8 pikseli dla graczy, zaś dwa dla pocisków...</p>
                    <p>Gdy już narysowałeś parę pikselków obiektu PMG, otwierają się nowe możliwości:</p>
                    <br>
                    <p>- Shift + "-", "=" zmienia jasność obiektu PMG;</p>
                    <br>
                    <p>- Shift + "+", "*" zmienia kolor obiektu PMG; Tu uwaga do tych dwóch czynności: zmieniany będzie tylko kolor bieżącego, wybranego obiektu PMG. Zmienianie kolorów PMG działa trochę inaczej, niż w przypadku kolorów "playfield". Ponieważ nowe kolory (PMG) nie są automatycznie umieszczane w każdej linii, zmiany w kolorach PMG będą we wszystkich liniach od pozycji kursora do dołu ekranu lub do innego miejsca, gdzie kolor PMG był poprzednio zmieniany nieco niżej na ekranie. Pewnie wygląda to nieco zagmatwanie, ale ( jak zwykle) praktyka w GED wszystko rozjaśni...</p>
                    <br>
                    <p>- Przesunięcie kursora na nową pozycję i wciśnięcie Shift + nr obiektu PMG, który edytujesz, spowoduje przesunięcie aktualnego duszka na nowe, wybrane przez Ciebie miejsce. Możesz przytrzymać Shift wraz z nr duszka i przesuwać kursor - jest to przydatne przy dopasowywaniu PMG do gotowego obrazka...</p>
                    <br>
                    <p>- Klawisz "&gt;" rozciąga duszka dwukrotnie, albo czterokrotnie (zależnie od wciskania tegoż), zaś "&lt;" powoduje jego skurczenie się aż do standardowych rozmiarów włącznie...</p>
                    <br>
                    <p>- rozmiary, położenie, kolor duszka można zmieniać co 1 linię ( o ile nie ma w danym miejscu większej ilości zmian rejestrów PMG; wówczas te zmiany mogą nastąpić dopiero co drugą, albo nawet co więcej linii... );</p>
                    <br>
                    <p>- wciśnięcie "T" (oznaczającego pokazanie tzw. palety testowej obrazu) da możliwość zobaczenia, gdzie na ekranie są obiekty PMG (będą one jednak w tym trybie nieco przesunięte w stosunku do normalnego ustawienia, ale to nic nie szkodzi !).</p>
                    <br>
                    <p>OK, tak więc wiesz już, jak utworzyć obiekt PMG... Teraz wszystko powinno pójść gładko.....</p>
                    <br>
                    <p>
                        <strong>Wypełnianie PMG:</strong>
                    </p>
                    <p></p>
                    <p>Chodzi tu oczywiście o odmianę komendy "Fill" dla duszków. Podobnie jak dla trybu "playfield", PMG także może być wypełniane na dwa sposoby - pełnym kolorem (tzw. solid fill) i 'kratką' (tzw. dithered fill). Obydwa sposoby działają jednak nieco inaczej w trybie "PMG" ( w porównaniu z "playfieldem"). Nie ma tu funkcji wypełniania zaznaczonego ramką obszaru w obiekcie PMG. Tryb wypełniania w wersji PMG po prostu kopiuje bieżące linie obiektu PMG do następnej linii ekranowej. Jak to zrobić:</p>
                    <br>
                    <p>- dla trybu 'pełnego' (solid) wypełniania:</p>
                    <br>
                    <p>1. Wciśnij "P", cyfrę z wybranym obiektem, umieść kursor w odpowiednim miejscu i naciśnij Shift + nr obiektu, który używasz, aby ustalić jego (duszka) początkową pozycję na ekranie;</p>
                    <br>
                    <p>2. Narysuj tym obiektem PMG linię, wciśnij spację, umieść kursor na narysowanej linii, wciśnij Fire i pociągnij joystick w dół (do siebie) - powinno zacząć się wypełnianie obiektu PMG od narysowanej pierwotnie linii aż na dół. Gdy skończysz, naciśnij spację, aby wyjść z trybu Fill.</p>
                    <br>
                    <p>- aby stworzyć 'kratkowane' wypełnienie w PMG:</p>
                    <br>
                    <p>1. Postępuj tak jak w punkcie 1. dla 'pełnego' wypełniania, tzn. ustaw duszka...</p>
                    <br>
                    <p>2. Narysuj obiektem PMG linię, w której widoczny będzie tylko co drugi piksel - będzie to coś na kształt ". . . ." (dla gracza z maksymalną szerokością będą widoczne 4 piksele);</p>
                    <br>
                    <p>3. Będąc w tej linii wciśnij spację i D oraz podaj z klawiatury numer 0-3 (nie przejmuj się tym, że chwilowo zmieni się położenie linii, którą narysowałeś). U góry ekranu pojawi się kratkowany prostokąt - symbol, że można już przystąpić do wypełniania... Ustaw kursor na narysowanej uprzednio linii, wciśnij Fire i pociągnij joystick do siebie - kratkowany wzór PMG zacznie się pojawiać... Po zakończeniu tego wypełniania wciśnij "D" (przywraca 'pełne' wypełnianie) oraz spację (wyjście z trybu Fill).</p>
                    <br>
                    <p>A teraz "czas na Colgate"... Sorry, to zgubny wpływ reklam... ;-) ... Oczywiście czas na...</p>
                    <br>
                    <p>
                        <strong>Brushes:</strong>
                    </p>
                    <p></p>
                    <p>...czyli po polsku, czas na pędzle, tudzież szczoteczki... Nas jednak nie interesują tutaj przedmioty do mycia zębów, lecz pomocne przybory malarskie... ;-))</p>
                    <p>GED pozwala na używanie (w ograniczonej formie) pędzli, których dane może kopiować z obiektów PMG na standardowy obraz ("playfield"). To narzędzie proste, lecz całkiem przydatne. Oto jak je używać:</p>
                    <br>
                    <p>- tradycyjnie zacznij od wciśnięcia "P", wybierz i ustaw duszka;</p>
                    <br>
                    <p>- narysuj nim dowolny kształt, ustaw kursor na jego szczycie (początku obiektu PMG), wciśnij "P"... Mała uwaga: pędzel może mieć dowolny kształt i wysokość, z tym, że pierwszą wolną (czystą) linię (od szczytu obiektu) GED uzna za koniec pędzla...;</p>
                    <br>
                    <p>- Wciśnij "B" - utworzony kształt z obiektu PMG zostanie zapamiętany w pamięci jako brush (pędzel). U góry ekranu pojawi się mały krzyżyk. Jest to oznaczenie trybu "pędzla". Teraz możesz, poruszając kursorem i naciskając Fire, powielać wielokrotnie kształt z "brusha" na ekran, używając aktualny kolor ("brushe" mogą być, niestety, tylko jednokolorowe);</p>
                    <br>
                    <p>- Wciśnij ponownie "B" lub spację, aby powrócić do normalnego trybu rysowania (wtedy utworzony kształt jest automatycznie kasowany z pamięci).</p>
                    <br>
                    <p>Inną, z interesujących rzeczy w GED, stanowi...</p>
                    <br>
                    <p>
                        <strong>Piąty gracz:</strong>
                    </p>
                    <p></p>
                    <p>Uzyskuje się go banalnie prosto - poprzez wspólne zgrupowanie wszystkich pocisków w jednym miejscu ekranu i skorzystanie z komendy "M"...</p>
                    <p>Sposób (z)użycia:</p>
                    <p></p>
                    <p>"P", po kolei ustawiamy obok siebie pociski (Shift + 5,6,7,8)... Bardzo ważne jest, by były one rzeczywiście jeden obok drugiego !!! Gdy już tak jest, najeżdżamy kursorem na tzw. "szczyt" (punkt początkowy), gdzie ma powstać piąty player i wciskamy "M" - pojawi się toto, mające niezależny od pozostałych czterech graczy kolor i pozostałe jak oni możliwości... Można też tak kombinować, że 5-ty graczy może być widoczny (włączony) tylko w paru liniach ekranu, natomiast nad nim, albo pod nim pociski mogą być rozdzielone (tak jak standardowo ). Jeśli zajdzie potrzeba przesunięcia piątego gracza w inne miejsce, a jesteś w 1. górnej linii ekranowej, to wystarczy przenieść kursor w inne miejsce tej linii i wcisnąć Shift+5 (normalnie odpowiada on za umieszczenie 1. pocisku, lecz gdy włączysz 5. gracza, to Shift+5 będzie sterował położeniem tego nowego duszka!) - wtedy zostanie ustawiona nowa pozycja piątego gracza. Dotyczy to tylko tej pierwszej linii ekranowej !!! Jeśli zechcesz ustawić piątego gracza gdzieś indziej, np. w środku ekranu, każdy pocisk musi być przesunięty indywidualnie - nawet wtedy, gdy opcja piątego gracza jest włączona !</p>
                    <br>
                    <p>Na razie jednak warto omówić...</p>
                    <br>
                    <p>
                        <strong>Priorytety (uporądkowanie) PMG:</strong>
                    </p>
                    <p></p>
                    <p>Najpierw przedstawię, co można zmieniać klawiszem "F" (priorytet PMG - "Playfield", czyli co [grafika "playfield", czy obiekt PMG] ma się pokazać "z przodu", jako widzialne, a co ma pozostać w ukryciu... :-)</p>
                    <p>W GED są możliwe do wyboru 4 tryby tego rodzaju priorytetu. Ponumerowałem je w kolejności wciskania klawisza "F" (pierwszy tryb jest automatycznie uruchomiony po załadowaniu GED'a), który to przełącza je po kolei...</p>
                    <br>
                    <p>1. PMG widoczne jest tylko na kolorze tła (kolor #0) i jest za kolorami "playfield" (#1,#2,#3), tzn. duszki są tam wtedy przysłonięte. Ten tryb jest włączonu i aktywny po uruchomieniu GED'a... Nie bez przyczyny akurat ten, gdyż jest chyba najlepszym do "uzupełniania" standardowej grafiki obiektami PMG. Wyjaśnię to szczegółowo na koniec tego artykułu. Czyli tutaj 1. priorytet = kolory "playfield" (wszystkie), a 2. priorytet = PMG 1-4.</p>
                    <br>
                    <p>- Info dla koderów: tu ustawiony jest bit drugi (dec #04) w komórce GTIACTL ($d01b).</p>
                    <br>
                    <p>2. PMG widać na kolorze tła i #3 kolorze "playfield". Na pozostałych kolorach PMG jest przysłonięte. Zatem 1. priorytet = kolory #0 i #1 "playfield", 2. priorytet = PMG 1-4 i 3. priorytet = kolory #2 i #3 "playfield".</p>
                    <br>
                    <p>- ustawiony jest bit 3. (dec #08) w GTIACTL</p>
                    <br>
                    <p>3. PMG można zauważyć na wszystkich kolorach "playfield" (#0, #1, #2, #3). Dlatego: 1. priorytet = PMG 1-4, 2. priorytet = kolory "playfield" #0-#3.</p>
                    <br>
                    <p>- ustawiony jest bit 0. (dec #01) w GTIACTL</p>
                    <br>
                    <p>4. Widoczne są najpierw duszki #0 i #1, następnie wszystkie kolory "playfield", a po nich duszki #2 i #3 (przysłonięte). Stąd: 1. priorytet = PMG 1-2, 2. priorytet = kolory "playfield" #0-#3, zaś 3. priorytet = PMG 3-4.</p>
                    <br>
                    <p>- ustawiony jest bit 1. (dec #02) w GTIACTL</p>
                    <br>
                    <p>Teraz czas na drugi rodzaj ustawialnych w GED priorytetów, uruchamianych klawiszem "O" (z ang. "Overlapping", czyli przesłanianie). Steruje to tym, jak mają się duszki "zachowywać" wobec siebie...</p>
                    <br>
                    <p>Są dwa typy tego priorytetu:</p>
                    <br>
                    <p>A. Przesłanianie (początkowo włączone w GED ). W tej "naukowej" tabelce pokazane jest, który PMG jest widoczny na którym...</p>
                    <pre>----------------------------------
\widocz-|PMG 1|PMG 2|PMG 3|PMG 4|
  ność  |     |     |     |     |
nr  \   |     |     |     |     |
----------------------------------
 PMG 1  |  X  |  +  |  +  |  +  |
----------------------------------
 PMG 2  |  -  |  X  |  +  |  +  |
----------------------------------
 PMG 3  |  -  |  -  |  X  |  +  |
----------------------------------
 PMG 4  |  -  |  -  |  -  |  X  |
----------------------------------

</pre>
                    <p>Oznaczenia:</p>
                    <p>"+" - PMG jest widoczny na tym obiekcie,</p>
                    <p>"-" - PMG nie jest widoczny na tym obiekcie  (jest przysłonięty przez inne PMG),</p>
                    <p>"X" - a to po prostu nic nie oznacza... 8-))</p>
                    <br>
                    <p>B. Nakładanie</p>
                    <p>Znacznie mniej rozbudowane od poprzedniego trybu priorytetu...</p>
                    <br>
                    <p>Polega na tym, że w miejscu gdzie nałożą się na siebie (częściowo lub całkowicie) duszki, odpowiednio 0 i 1 oraz 2 i 3, kolor ich części wspólnej będzie równywartości OR ich kolorów. Mówiąc trochę prościej, gdy nastąpi nałożenie dwóch graczy, to ich część wspólna otrzyma kolor powstały w wyniku operacji logicznej ORA na dwóch kolorach tych graczy. Normalnie duszek może mieć tylko jeden własny kolor. Jeśli jednak "skrzyżuje się" go z innym duszkiem, to wykonując odpowiednią instrukcję ORA, otrzyma się 3-kolorowego duszka (ten dodatkowy, trzeci kolor jest efektem nakładania się dwóch pozostałych...). Ten priorytet (bit 5. w GTIACTL) nazywany jest czasem graczem wielokolorowym. Teraz chyba już wszyscy wiedzą o co chodzi... (?).</p>
                    <br>
                    <p>Tutaj dwie uwagi do wprowadzania zmian w priorytetach (klawiszami "O" i "F"):</p>
                    <br>
                    <p>- po każdorazowym załadowaniu grafiki albo czyszczeniu obrazu (Shft+Ctrl+Tab) GED przywraca początkowe wartości w priorytetach (włączony zostaje 1. priorytet PMG-"Playfield", itd. );</p>
                    <br>
                    <p>- Zmiany w priorytetach działają linię niżej (co NAJMNIEJ, jeśli nie ma dużej ilości zmian rejestrów w tym miejscu) od miejsca ustawienia !</p>
                    <br>
                    <p>
                        <strong>Umieszczanie PMG:</strong>
                    </p>
                    <p></p>
                    <p>Wciśnięcie klawisza Shift+1-8 ustawia poziomą początkową pozycję obiektu PMG, odpowiadającą aktualnej pozycji kursora. To działa trochę odmiennie w zależności od tego, czy kursor jest umieszczony na 1. linii u góry ekranu, czy też gdziekolwiek indziej poniżej. W pamięci istnieje tabela, która przechowuje początkowe atrybuty (właściwości) dla wszystkich rejestrów PMG. Są w niej dane kolorów, priorytetów, szerokości i pozycja 1. duszka. Pozycja drugiego duszka otrzymywana jest przez dodanie do pierwszego jego szerokości. Podobnie jest z trzecim i czwartym duszkiem. Następne w kolejności są pociski. Przed wyświetleniem obrazka wartości z tej tablicy są przepisywane do rejestrów sterujących PMG. W każdej linii ekranowej można zmienić jedną z wartości sterujących PMG. Jeśli zrobisz się to stojąc w 1. linii (gdzie znajduje się tablica atrybutów), to wartość ta będzie wpisana do tablicy. Oznacza to, że w 1. linii można zmienić wszystkie wartości, natomiast w pozostałych, niższych liniach tylko jedną. Jeśli więc najpierw w jakiejś linii zmienisz kolor duszka, a następnie w tej samej linii jego szerokość, to ta zmiana koloru nie zostanie w tej linii uwzględniona. Inaczej będzie w 1. linii ekranowej, gdzie obydwie zmiany będą uwzględnione. Praktycznie rzecz biorąc, to, że 1. linia obrazu ma takie korzyści, dużo nie daje, skoro reszta linii ma dużo mniejsze możliwości... Ale warto wiedzieć o tej różnicy... Acha, pisząc "1. linia obrazu", mam na myśli pierwszą linię na górze ekranu, gdzie można rysować, umieszczać obiekty PMG, itd. (a nie sam szczyt ekranu, powyżej ikon informacyjnych GED'a !)...</p>
                    <br>
                    <p>Jeśli nie zrozumiałeś dobrze powyższego tekstu o tabeli wartości PMG w GED i ograniczeniach w modyfikacji rejestrów duszków, to... spróbuję to przedstawić trochę inaczej, jeszcze raz, poniżej.</p>
                    <br>
                    <p>Zmiany w rejestrach PMG nie są automatycznie umieszczane w każdej linii obrazu i taka zmiana rejestru PMG będzie działać (będzie widoczna) w każdej linii, od pozycji kursora, aż do samego dołu ekranu, lub do miejsca poniżej, gdzie ten rejestr był później zmieniany. Dlatego zmiany w PMG działają nieco inaczej w porównaniu z trybem "playfield".</p>
                    <p></p>
                    <p>Wszystkie atrybuty PMG mają swe wartości początkowe w specjalnej tablicy, która mieści się na szczycie ekranu (tzn. w 1. linii ekranowej). Kiedy kursor jest na samej górze, gdy podajesz programowi jakąś komendę sterującą PMG, ta zmiana zajdzie w tejże tablicy i możesz zmieniać wszystkie wartości atrybutów (właściwości) PMG w ten sposób (Shft + Ctrl + "-" przydaje się, aby przejść na samą górę ekranu). Zatem można tu zmieniać kilka parametrów PMG naraz.</p>
                    <p></p>
                    <p>Jeśli jednak kursor jest częściowo na dole ekranu, każda komenda dla PMG będzie musiała używać procedury przerwania DLI, która może zmieniać tylko jeden atrybut (np. szerokość duszka) naraz. Po prostu na tylko tyle (dla PMG) pozwala czas w procedurze DLI. Jeśli wprowadzisz jeszcze jedną (inną) komendę dla PMG w tej samej linii, GED będzie szukał najbliższą NIEUŻYWANĄ (jest to linia, która nie zawiera zmiany rejestru PMG; linia ta może zawierać dane koloru "playfield" lub dane obiektu PMG) linię obrazu POWYŻEJ pozycji, którą edytujesz. Kursor zostanie przeniesiony na tę znalezioną, wolną linię, aby dać Ci znać, gdzie została umieszczona komenda. Jeżeli GED natrafi na szczyt ekranu (1. linię ekranową) albo będą sprzeczne (konfliktowe) komendy przed znalezieniem nieużywanej linii, obraz mrugnie krótko, aby poinformować Cię, że ta komenda nie mogła być wykonana. Kursor zostanie umieszczony na konfliktowej pozycji.</p>
                    <br>
                    <p>
                        <strong>Problemy:</strong>
                    </p>
                    <p></p>
                    <p>... są nieodzownym elementem tego świata. Oczywiście nie mogło ich zabraknąć także w GED... ;-)). GED, jako chyba pierwszy program, stosujący nową technikę łączenia wielokrotnych zmian kolorów w linii ekranowej z pełnym wykorzystaniem możliwości PMG, ma także pewne ograniczenia, wynikające po prostu z ograniczeń sprzętowych...</p>
                    <p></p>
                    <p>Podczas nakładania PMG na kolory "playfield" (wraz ze zmienianiem któregoś z priorytetów) może się zdarzyć, że gdy zapragniemy coś zmienić (np. przenieść lub wykasować) w dokonanej komendzie na PMG, okaże się to (z pozoru) niemożliwe. Szczególnie dotyczy to pocisków. Po prostu mogą "nie chcieć" dać się ponownie zedytować w danym miejscu. Trzeba wtedy próbować różnych kombinacji - zmiany priorytetów, usunięcia najpierw koloru "playfield" z pozycji na której jest duszek, itd. Powinno się udać, tyle że po pewnych staraniach... ;-)</p>
                    <p></p>
                    <p>Możesz spotkać się z innym problemem, polegającym na tym, że jeśli masz dużą liczbę zmian rejestrów, do czasu gdy GED znajdzie 'nieużywaną linię' (dobrą do zmiany jednego z rejestrów PMG), może być to dość daleko powyżej Twojej pozycji kursora. Wtedy lepsze może okazać się zmienianie innego rejestru i zostawienie tego poprzedniego w "spokoju"... Np. powiedzmy, że masz dwa małe obiekty na ekranie (wypełnione jednym kolorem "playfield" kwadraty, jeden pod drugim), które próbujesz podkolorowć z użyciem PMG. Te obiekty są oddzielone jedną wolną linią skanową (ekranową) między sobą. Wciśnij "P", 2x "F" (zmiana priorytetu - aby PMG pokazało się na kolorach "playfield"), ustaw kursor na lewy górny róg niższego obiektu i wciśnij Shift + 1, by przesunąć gracza na nowe miejsce. "Wpixeluj" duszka i wtedy użyj Shft + strzałki w celu zmiany koloru tego obiektu (zrób to będąc na "szczycie" duszka). Ponieważ ta linia obrazu była już użyta do przechowania zmiany pozycji PMG, GED użyje pustą (wolną) linię między tymi dwoma obiektami. Teraz decydujesz, że drugi (niższy) obiekt musi być większy i potrzebujesz zrobić szerszego gracza, by "zakryć" niższy obiekt. Kiedy wciśniesz "&gt;" w tym punkcie (tzn. w 1. linii drugiego obiektu, albo w pustej linii między obiektami), najbliższa wolna linia (dla zmiany rejestru PMG) jest na samym dole 1. obiektu i zmienianie tam gracza, może zmienić wygląd 1. obiektu... Gdy zachodzi coś takiego, możesz najpierw wcisnąć Shift + 0, aby skasować tą ostatnią zmianę rejestru (niekorzystną dla 1. obiektu). Powinieneś wtedy jeszcze sprawdzić obraz, aby zobaczyć, czy są inne sposoby osiągnięcia tego, czego chcesz. Może się okazać, że nie potrzebujesz dodatkowej szerokości dokładnie w tym miejscu i możesz ją wprowadzić trochę dalej, poniżej tego obiektu. Może także nie być sposobu na zrobienie tego, czego chcesz i jedynym wyjściem jest przejść do edycji innego obiektu, albo zmienić coś w aktualnie 'obrabianym' obiekcie.</p>
                    <p></p>
                    <p>Są jeszcze inne rzeczy, które możesz robić w "ciasnych" miejscach, włącznie z edytowaniem lub nieznacznym przesuwaniem obiektów w celu umożliwienia zmian rejestrów i umiejętnym 'krzyżowaniem' PMG z 'komórkami koloru' trybu "playfield".</p>
                    <p></p>
                    <p>Inną sprawą jest to, że jeśli nowa zmiana koloru jest stosunkowo blisko do poprzedniej wartości koloru i nie możesz dokonać tej zmiany dokładnie na pierwszym pikselu, gdzie potrzebujesz koloru, może być ona całkowicie niezauważalna. Ludzie mogą nawet nie zauważyć kilku pikseli w odmiennym kolorze. Ten efekt występuje raz na obrazku "MARTIAN.GED". Czy możesz tam odnaleźć to miejsce ?</p>
                    <br>
                    <p>
                        <strong>Wskazówki do kolorowania:</strong>
                    </p>
                    <p></p>
                    <p>Standardowy tryb priorytetu PMG w GED jest ustawiony tak, aby rysować obiekty PMG za standardowym ("playfield") obrazem. W tym trybie obiekty PMG będą widoczne tylko we fragmentach obrazka, które są "wyczyszczone" (tzn. tam, gdzie jest kolor tła). To jest często najlepsze rozwiązanie, bo możesz tworzyć duszki z maksymalną szerokością i 'maskować' je z przodu którymś z kolorów "playfield" na całym ekranie. Zauważ, ze gdy pociski są jako 5-ty gracz, to tenże obiekt PMG (5. gracz) pojawi się "z przodu" wszystkich kolorów "playfield", bez względu na ustawione priorytety.</p>
                    <br>
                    <p>Na tym pragnąłbym zakończyć ten (przydługi) opis edytora "GED"... Mam nadzieję, że zachęciłem trochę osób do jego używania i oszczędziłem im męki samodzielnego 'rozgryzania' GED'a, której to "przyjemności" osobiście doświadczyłem. Przygotowując ten opis korzystałem z oryginalnej instrukcji do GED'a autorstwa J.Harrisa oraz sporej ilości własnych spostrzeżeń odnośnie GED.</p>
                    <br>
                    <p>Dodatkowym plikiem do tego artykułu jest "GEDSTUF2.ARC", w którym jest parę ciekawych obrazków, demonstrujących wykorzystanie GED'a w praktyce. Zawarłem tam też dodatkowe uwagi o GED...</p>
 
 </p>
 </p>
 </p>
 </p>
 </p>
 </p>
 
</html>

<hr>

## GED viewer

<html>

<div style="float: right">
<img src="../gfx/jaskier.jpg" alt="jaskier" width="80" height="117"><br>autor: jaskier
<br>
</div>

<p>
Wielu z Was zapewne słyszało o pewnym
programie graficznym, zwanym skrótowo
GED. Napisany został on w 1993 roku przez
Johna Harrisa. Jest to program, który pod
względem możliwości graficznych znajduje
się gdzieś w pierwszej piątce wszystkich
programów graficznych na Atari. Również
pod względem ilości wbudowanych opcji
ten program znajduje się w pierwszej
piątce, tyle że od tyłu.

<br><br>

Jednak, mimo braku nawet najbardziej
elementarnych opcji, program jest szeroko
używany przez grafików różnych maści.
Jest to spowodowane tym, że program
udostępnia chyba najwięcej (na oko jakieś
20%) możliwości graficznych Atari, spośród
wszystkich innych programów graficznych.

<br><br>

Pomysł, aby nie tylko zmieniać kolory co
linię, ale również w jej środku, a ponadto
dodać pełnię możliwośći PMG, oddzielne dla
każdego ghosta kolory i szerokości,
priorytety i inne zabawki, jest wspaniały.
Naprawdę wielkie brawa dla Johna Harrisa.

<br><br>

Ach gdyby nie ta zapierająca dech obsługa.

<br><br>

Program niestety posiada również inną
wadę, ujawniającą się niestety najpóźniej,
bo już po narysowaniu całego obrazka.
Do programu mianowicie nie dołączono
procedury, którą można by umieścić we
własnym programie, aby pokazać w nim
własny obrazek narysowany w GED-zie. Tą
niedogodnością jakiś czas temu zaciekawił
mnie Dracon/USG/Taquart. Poprosił mnie
mianowicie (po tym jak odmówił mu Konop i
paru innych koderów) o napisanie takiej
procedury, gdyż potrzebował jej do
swojego slideshowu. Po przejrzeniu GED-a
za pomocą wszystkich dostępnych mi
debuggerów (z których każdy niestety
pokazywał to samo) zabrałem się do pracy.

<br><br>

Oto wynik moich poszukiwań. (Pełny tekst
programu znajduje się w zarchiwizowanym
pliku jako GEDVIEW.ASM.)

<br><br>

Dane program trzyma od adresu $5330,
do adresu $7F4F. Zapisywane jest to
jednym ciągiem w formacie DOS-owym to
znaczy z bajtami $FFFF, $5330, $7F4F na
początku.

<br><br>

Zmieniając adres danych można zmieniać
tylko pierwszą cyfrę, gdyż Antic ma głupi
zwyczaj dane obrazka pobierać tylko z
czterech kilobajtów.

<br><br>

Kilka linii przed początkiem obrazka
zaczyna się przerwanie. Jest ono
docyklowane z dokładnością do 0.001 cykla,
tak więc należy zwracać uwagę na to, że:

<br><br>

Mój program został przystosowany do
umieszczenia na początku strony. Wszelkie
zmiany tego położenia, a także wszelkie
zmiany w programie mogą zmienić położenie
pętli umieszczonych w przerwaniu. Pętla,
której początek i koniec znajdują się na
dwu różnych stronach może znaleźć się na
jednej stronie, a tym samym rozkaz skoku
na początek pętli (bpl) będzie działać o 1
cykl krócej. Należy również uważać na to,
że display list musi znaleźć się cały w
jednym kilobajcie. Ponadto zaraz za
programem należy zostawić 10KB wolnego,
gdyż umieszczany jest tam program
przerwania generowany dopiero po
uruchomieniu mojej procedury.

<br><br>

Oto skrócony opis programu, dla tych,
którzy chcieliby poznać sposób, w jaki
pokazuje się obrazki z GED-a.

<br><br>
Najpierw opis danych:
<br><br>

Osiem tablic po 200 bajtów zawiera
dane zmian kolorów itp. robionych co linię:
<br>

- tb2, tb3, tb4, tb5, tb6, tb7, tb8, tb9  dane
 ośmiu zmian kolorów w linii, kolejno:
 kolor 1, 2, 3, 1, 2, 3, 1, 2.

<br><br>
Oprócz tych zmian można dokonywać
również co linię jednej ze zmian w ghostach
(kolor, szerokość itp.) lub koloru tła.
Wartości tych zmian zawiera tablica tb0, zaś
komórki, które trzeba zmieniać tablica tb1.
<BR>
<BR>
-dane- szesnaście komórek:

<TABLE WIDTH=100% BORDER=0 CELLPADDING=5 CELLSPACING=0>
	<TR VALIGN=TOP>
		<TD WIDTH=10%>
0,1,2,3<br>
4<br>
5<br>
6<br>
7<br>
8<br>
9,10,11,12<br>
13<br><br>
14<br><br>
15<br>
		</TD>
		<TD WIDTH=90%>

kolory wpisywane do $d012-$d015<br>
szerokości playerów (po dwa bity od najstarszych wpisywane do $d008-$d00b)<br>
szerokości missilów ($d00c)<br>
priorytety ($d01b)<br>
kolor missilów (do $d019)<br>
kolor tła ($2c8 lub $d01a)<br>
położenia poziome graczy (komórki od $d000 do $d003)<br>
położenie poziome pierwszego missila, do pozycji następnych dodawana jest szerokość poprzedników<br>
numer opóźnienia przerwania i tym samym miejsca zmiany kolorów. W GED-dzie ustawia się to klawiszami [,] i [.])<br>
nieużywane.
		</TD>
	</TR>
</TABLE>



<br>
-obr1,obr2- dane obrazka podzielone na
dwie części z powodu pewnej wady Antica.

<br><br>

 A teraz opis kilku części programu:


<PRE>
   lda &GT;pmg-$300 pierwsze 3 strony nie są
   sta $D407     używane, więc stąd ten adres.

   lda &LT;end      Generuje początkowe
   sta addr      bajty umieszczane za
   lda &GT;end      etykietą END. Najpierw
   sta addr+1    na podstawie dane+14
   lda dane+14   umieszczane są 4 bajty,
   asl @         które nic nie robią, ale
   asl @         dają różne opóźnienie.
   adc #3        Owe czwórki bajtów
   tax           umieszczone są pod
   ldy #3        etykietą proc3.
s1 lda proc3,x
   sta (addr),y
   dex
   dey
   bpl s1
</PRE>

<p>
 Teraz adres jest zwiększany o 4:
 
<PRE>
   lda &LT;end+4
   sta addr
   lda &GT;end+4
   sta addr+1
</PRE>

<p>
i dalej będzie procedura generująca 200
razy prog. zmieniający kolory w każdej linii.
 (Jest za długa aby ją tu umieszczać.)
 Składa się ona ze zwykłego przepisania
wartości z tablic, tak aby przerwanie nie
marnowało czasu na długie rozkazy typu:

<PRE>   lda tb4+175</PRE>

<p>
 ale zadowalało się rozkazami typu:

<PRE>   lda #$16</PRE>

<p>
 (wartość $16 została wcześniej pobrana z
tablicy tb4+175). Zysk: 1 cykl.

<br><br>

 Każdy fragment przerwania kończy się
rozkazem inc 0, które nie ma niczego robić,
ale tylko zająć 5 cykli, tak aby czas
tworzenia 1 linii przez Antic był równy
czasowi wykonywania tego fragmentu
przerwania przez procesor. Jednakże,
pamięć obrazka została podzielona na dwie
części i kiedy Anticowi podaje się do żarcia
tę drugą część (w dliście wygląda to jak:
dta b($4e),a(obr2)), to procesor ma o 2

<pre>
   pla              cykle mniej czasu.
   clc              Należy więc zmienić ten
   adc #1           rozkaz na lda 0, który
   cmp #$66         zajmuje 3 cykle.
   bne s4           Ten program rozpoznaje
   pha              właściwy wiersz i
   dec addr+1       dokonuje drobnej zmiany
   ldy #$fe         (bajt $a5) w już wygene-
   lda #$a5         rowanym fregmencie
   sta (addr),y     programu.
   inc addr+1
   pla
s4 cmp #$c8         a tu sprawdza, czy to już
   bne s2           wszystkie linie.
   ldy &LT;proc3-proc2 z kolei tutaj
s5 lda proc2,y      generowana jest
   sta (addr),y     procedura
   dey              wyjścia z
   bpl s5           przerwania.

   lda dane+5       Ten fragment programu
   ldx #0           jest o tyle ciekawy, że
   ldy #$ff         wykorzystany jest tutaj
s6 iny              nic nie robiący rozkaz
s7 lsr @            bit $4a. Kiedy jednak
   bcc s9+1         wykonamy skok w bajt
   lsr @            stanowiący operand $4a
   bcc s8           to wykona się rozkaz
   inx              lsr @. Pozwala to znacznie
   inx              skrócić program. Polecam
   inx              tę sztuczkę każdemu.
   inx              Ten fragment akurat
s8 inx              dokonuje ustawienia
   inx              położeń pocisków na
s9 bit $4a          podstawie dane+5 oraz
   inx              ich szerokości. Ponieważ
   inx              to nieistotne część
   pha              programu wyrzuciłem:
   ...
   ...
   pla              (akurat tę zapisującą
   cpy #3           już wartości) i zostawiłem
   bne s6           wyjście z pętli.
</pre>

<p>
 Teraz rzecz najgorsza, czyli programy
pracujące w przerwaniach. Na początek
procedury przepisywane. (Patrz wyżej.)
<br><br>

-PROC1 to procedura wygenerowywana 200
razy. Była już o niej mowa wcześniej.<br>
-PROC2 to procedura kończąca przerwanie.<br>
-PROC3 zawiera kilka 4-bajtowych procedur
służących ustawieniu (z dokładnością do 1
cyklu) miejsca zmian kolorów. Kazda 4-ka
bajtów różni się czasem wykonywania.<br>
-DL tu się zaczyna przerwanie. Zwykłe
ustawianie wartości itp. Jedyny ciekawy
fragment to:

<pre>
   ldx #11          ciekawy dlatego, że nic nie
   dex              robi. Chodzi tutaj jedynie o
   bne *-1          przeczekanie trochę cykli
   lda (0,x)        aż sprawa nie przycichnie...
   lda 0            tfu... co ja mówię!!!

end equ *
</pre>

<p>
         od tego miejsca wpisywane
są poszczególne procedury: 4 bajty wzięte
z PROC3, następnie 200*PROC1, a w końcu
PROC2.<br><br>

 Jak widziecie metoda pokazywania
obrazków stworzonych GED-em (gadem?)
jest dość prosta.

<P ALIGN="RIGHT"> JASKIER/TAQUART

</html>