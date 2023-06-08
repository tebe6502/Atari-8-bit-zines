#

## Opis formatu Music ProTrackera

<html>

<div style="float: right">
<img src="../gfx/mayonez.jpg" alt="mayonez" width="80" height="117"><br>autor: mayonez
<br>
</div>

<p>Ostatnimi czasy wśród programów muzycznych na naszą kochaną maszynkę króluje niewątpliwie "Music Protracker v.2.4" zwany w skrócie MPT. Mimo kilku wkurzających wad, jest to dobry program, przewyższający swoimi możliwościami brzmieniowymi CMC. Niestety w momencie wypuszczenia tego programu grupa "Slight" poza instrukcją obsługi nie udostępniła opisu formatu plików obsługiwanych przez ten program. Zdegustowany tym faktem, "pogrzebałem" nieco w muzyczkach z MPT i ostatecznie "rozgryzłem" ten format. Poniżej znajduje się dokładny opis formatu plików z MPT v2.4. Format ten opisuję na ramach "Energy Zine", gdyż zdaję sobie sprawę z tego, że większość scenowców nie zna tego formatu. Znajomość formatu MPT może zaowocować powstaniem na scenie różnych konwerterów itp.</p>
<p></p>
<p>Równocześnie zdaję sobie sprawę z tego, że okres panowania MPT na scenie minie wraz z pojawieniem się nowych, doskonalszych programów muzycznych, wykorzystujących drugiego Pokeya. Upłynie jednak jeszcze trochę wody w klozecie, zanim takowe programy ujrzą światło dzienne. (Od redakcji: w czasie pisania tego artykułu autor nie miał jeszcze pojęcia o istnieniu TMC.)</p>
<p></p>
<p>Póki co, musimy zadowolić się i tak dobrym MPT, który stał się już swoistym standardem na Scenie. No, ale dość już przynudzania. Przejdźmy do rzeczy.</p>

<div class="hr">MPT v2.4 file format:</div>
<p></p>
<p><strong>1. Struktura pliku. Nagłówek</strong></p>
<pre>   offset
   od - do - opis
   (HEX)</pre>
<p><strong>$0000</strong>-<strong>$003F</strong> - adresy brzmień (LSB/MSB) (32 słowa). Bajty <strong>$00</strong>, <strong>$00</strong> w tej tablicy oznaczają, że dane brzmienie jest puste</p>

<p><strong>$0040</strong>-<strong>$00BF</strong>- adresy patternów (LSB/MSB) (64 słowa). Bajty <strong>$00</strong>, <strong>$00</strong> w tej tablicy oznaczają, że dany pattern jest pusty</p>

<p><strong>$00C0</strong>-<strong>$01BF</strong> - cztery tablice częstotliwości  (64 bajty każda)</p>

<p><strong>$01C0</strong>-<strong>$01C3</strong> - młodsze bajty adresów  tracków</p>

<p><strong>$01C4</strong>-<strong>$01C7</strong> - starsze bajty adresów  tracków</p>

<p><strong>$01C8</strong>-<strong>$01C8</strong> - długość patternów  (wartości - <strong>$10</strong>, <strong>$20</strong>, <strong>$30</strong> lub <strong>$40</strong>)</p>

<p><strong>$01C9</strong>-<strong>$01C9</strong> - tempo utworu</p>

<p><strong>$01CA</strong>-? - dane tracku #1, dane tracku #2, dane tracku #3, dane tracku #4</p>

<p>Ilość danych dla jednego tracku zależy od różnicy pomiędzy adresami sąsiednich tracków</p>

<p>?-? - dane brzmień</p>

<p>?-? - dane patternów</p>

<p><strong>2. Dane brzmień.</strong></p>

<p>Brzmienie ma długość 48 bajtów, jeśli nie jest puste.</p>

<p>Pierwsze 32 bajty układają się w pary:</p>

<p>BG PN.. (x16)</p>

<p>gdzie:</p>

<p>B - barwa dzwięku - 4 bity (starsze)</p>

<p>G - głośność dźwięku - 4 bity (młodsze)</p>

<p>P - numery parametrów akcentów pomnożone  przez 2 (drugi rząd) - 4 bity  (starsze)</p>

<p>N - numery akcentów (pierwszy rząd) -  4 bity (młodsze)</p>

<p>następne 8 bajtów to parametry sterujące instrumentem (pierwszy rząd z lewej)</p>

<p>kolejne 8 bajtów to parametry akcentów (drugi rząd z lewej)</p>

<p><strong>3. Dane Patternów.</strong></p>
<pre>   bajt (N) działanie
   wartość
   w zakresie:
</pre>
<p><strong>$0</strong>1-<strong>$3E</strong> - granie nuty (a raczej  półtonu) o numerze N  (np. 1=C-1, 2=C#1, 3=D-1)</p>

<p><strong>$40</strong>-<strong>$5F</strong> - zmień brzmienie na numer  równy N-<strong>$40</strong></p>

<p><strong>$80</strong>-<strong>$BE</strong> - ustaw ilość odstępów  pomiędzy nutami na N-<strong>$80</strong></p>

<p>działa dopiero po odegraniu nuty (od momentu wystąpienia rozkazu pierwszy odstęp pojawia się za nutą)</p>

<p>Jeśli zaraz za tym bajtem (kodem) występuje bajt równy $FE następuje ustawienie pustych pozycji w patternie. Ilość tych pozycji wynosi N-<strong>$7F</strong>. W tym przypadku puste pozycje pojawią się od razu, w momencie wystąpienia bajtu <strong>$FE</strong>, np. ciąg bajtów:</p>
<pre>$83 $FE $41 $81 $01 $03 $01 $05
 | | | | | | | |
 | | | | --numery półtonów
 | | | |
 | | | 1 odstęp pomiędzy nutami
 | | |
 | | ustaw brzmienie #1
 ----
 |
4 puste pozycje na początku patternu

</pre>
<p>reprezentuje pattern:</p>
<pre>--- --
--- --
--- --
--- --
C-1 01
--- --
D-1 01
--- --
C-1 01
--- --
E-1 01
--- --

</pre>
<p>Pominięto głośność brzmień.</p>

<p><strong>$C0</strong>-<strong>$CF</strong> - ustaw głośność nut na  równą N-<strong>$C0</strong></p>

<p><strong>$D0</strong>-<strong>$DF</strong> - ustaw tempo grania na  równe N-<strong>$D0</strong></p>

<p><strong>$Ex</strong> - koniec patternu  (x - dowolne 4 bity)</p>

<p>UWAGA !!! - MPT v2.4 zapisuje w pliku  patterny w ten sposób, że  zawsze mają stałą długość,  równą ustawionej w nagłówku.  Następuje to poprzez dodanie  na końcu patternu rozkazu  tworzącego puste pozycje, tak  aby każdy pattern miał  identyczną liczbę pozycji.</p>

<p>UWAGA #2 !!!</p>

<p>Wpisując dane w trackach w MPT należy zwrócić uwagę na to, aby rozkaz skoku lub rozkaz zatrzymania utworu (odpowiednio $FF i $FE) znajdowały się na ścieżce numer 0, a wartości na pozostałych ścieżkach były równe 0. W przeciwnym wypadku MPT błędnie obliczy adresy brzmień i patternów podczas zapisywana pliku. Muzyczka zapisana w ten sposób będzie się poprawnie wczytywała do MPT, natomiast podczas odgrywania tejże muzyczki za pomocą jakiegoś playera usłyszymy tylko bulgoty albo ciszę.</p>

<p><strong>MODUŁ SAMPLI z MPT v2.4</strong></p>
<p></p>
<p>UWAGA !!! - TO NIE JEST PLIK BINARNY  (DOSOWY)</p>

<p>od-do opis</p>

<p><strong>00-0F </strong>- starsze bajty adresów początku  sampli</p>

<p><strong>0F-1F</strong> - starsze bajty adresów końca  sampli (zwiększone o 1)</p>

<p><strong>1F</strong>-? - Dane sampli</p>

<p>UWAGA !!! - adresy sampli w nagłówku  zaczynają się nie od <strong>$0000</strong>,  ale od <strong>$9000</strong> (adres bufora  na sample w MPT)</p>

<p>Tak, i to na tyle. Mam nadzieję, że przedstawiony powyżej opis formatu plików MPT przyda się komuś.</p>

<div class="hr">Plik do ściągnięcia:

</div>
<img src="../gfx/floppyicon.gif" border="0"><a href="download/mpt24s.zip">mpt24s.zip</a> <br>

</div>
</div>

</html>

<hr>


## IRQ Loader

<html>

<div style="float: right">
<img src="../gfx/jaskier.jpg" alt="jaskier" width="80" height="117"><br>autor: jaskier
<br>
</div>

<p>
 Czołem towarzysze. Tak jak
obiecywaliśmy w naszym magazynie
znajdziecie wiele pożytecznych informacji i
programów, które mogą się przydać przy
tworzeniu własnych programów użytkowych
oraz dem. W tym artykule akurat znajduje
się coś pożytecznego dla twórców dem.
<br><br>

 Proces ładowania, to w demach
newralgiczne miejsce. Chciałoby się ten
czas wykorzystać, podobnie jak w demach
na C64, na jakieś efekty. Niestety
standardowa procedura na to nie pozwala.
Zajmuje po prostu cały czas procesora,
chociaż przez większość czasu oczekuje w
pętli na ustawienie się jakiś znaczników.
<br><br>

 O tym, że można inaczej, przekonują
nas przykłady takich dem jak Overmind.<br>
Podczas ładowania pokazują się tam efekty,
gdyż cała procedura ładowania realizuje
się w przerwaniach IRQ. Podobnie jest w
przypadku magazynu Energy. Ponieważ zaś
nigdy nie robimy tajemnic z naszych
rozwiązań (pod warunkiem, że sami
wykorzystaliśmy je już dużo wcześniej), więc
postanowiliśmy przedstawić tutaj nasz
sposób. 
<br><br>

Za źródło niech posłuży nam
loader użyty w Energy #1 do ładowania
intra. Znajduje się on tam w trzech
pierwszych sektorach dysku. Wszystkie
inne używane przez nas IRQ-loadery są w
istocie bardzo podobne do tego. A zatem
zaczynamy.
<br><br>

 Loader przystosowany jest na
sektory po 128 bajtów. Plik zaś zapisany
jest w sektorach o strukturze DOS-owej
(ostatnie 3 bajty sektora nie stanowią
danych pliku). Sam plik zaś również ma
strukturę DOS-ową. Ponadto, ponieważ nie
używamy systemu, więc absolutnie się nim
nie przejmujemy wyłączając ROM i używając
dolnej części strony zerowej. Ponieważ
dysk na którym ten loader miał być
nagrany był całkowicie w formacie
DOS-owym, więc musiałem dokonać paru
karkołomnych sztuczek, aby loader zmieścił
się w tych wyznaczonych 3 sektorach.
Zmniejsza to czytelność programu. Trudno.
<br><br>

 Autorem IRQ-SIO jest Electron, zaś
cołości loadera Jaskier.
</p>

<pre>
* IRQ-SIO Loader

bufor equ $680 ; 128 bajtów na dane odczytane z sektora.

dcb equ 0      ; 4 bajtowy bufora na dane wysyłane do stacji dysków.
               ; Jest to kolejno:
               ; -bajt identyfikujący urządzenie. Każde
               ; urządzenie: D1,D2,D3,D4,P1,P2,R1 itd. ma
               ; własny kod.
               ; -kod operacji. Dokładnie taki sam jak w operacjach SIO.
               ; -numer sektora. Młodszy i starszy bajt.

cksum equ 4    ; używane do liczenia sumy kontrolnej zarówno przy 
               ; wysyłaniu komendy do stacji, jak i przy odbiorze.

xdone equ 5    ; stan loadera:
               ; 0   - odczytywane są dane bloku,
               ; 1-4 - odczytywany jest nagłówek bloku.

lindex equ 6   ; stan przy wysyłaniu komendy do stacji:
               ; 0-3 - wysyłanie tablicy dcb,
               ; 4   - wysyłanie sumy kontrolnej,
               ; 5   - wywołanie przerwania końca transmisji.

stcnt equ 7    ; stan przy odczycie sektora:
               ; $fe - odczytany został pierwszy bajt od
               ; stacji. Jeśli jest to wartość $41, to znaczy,
               ; że stacja prawidłowo odebrała komendę.
               ; $ff - drugi bajt. Jeśli jest to $43, to znaczy,
               ; że sektor na dysku został prawidłowo
               ; odczytany. Przystępujemy do transmisji.
               ; 0-127 - dane sektora.
               ; 128 - bajt sumy kontrolnej.

adr equ 8      ; adres początku bloku.
end equ 10     ; adres końca bloku.

 org $500

loader dta b(0),b(3),a(loader),a(4)

start sei
 cld
 jsr del       ; skok do procedury przygotowującej stację do wysłania komendy
 stx $d40e     ; w X jest 0
 stx $d400
 lda #$fe
 sta $d301

 lda #$52      ; komenda odczytu sektora
 sta dcb+1
 lda #4        ; numer pierwszego sektora
 sta dcb+2     ; odczywywanego pliku
 lda #$28      ; ustawiamy częstotliwość zegara
 sta $d204
 sta $d208
 stx $d206
 stx dcb+3
 inx           ; najpierw będziemy odczytywać
 stx xdone     ; nagłówek bloku

 lda <irq
 sta $fffe
 lda >irq
 sta $ffff
 jsr set       ; rozpoczęcie wysyłania komendy
 cli
 bne *         ; a tu każdy może wsadzić nawet
               ; wektorówkę (jeśli potrafi)
               ; P.S. ten rozkaz BNE oznacza tyle co JMP

init jmp ($2e2); plik może mieć inity

del lda #$34   ; informujemy stację, że coś do
 sta $d303     ; niej będziemy wysyłać
 ldx #0        ;  ustawienie licznika wysyłanych
 stx lindex    ; bajtów
 inx           ; czekamy trochę, aż stacja
 bne *-1       ; przetrawi fakt, że coś od
 rts           ; niej chcemy. Niestety nie
               ; można skrócić tej pętli, gdyż niektóre
               ; stacje są bardzo powolne np. Tygrys Turbo

set lda #$23   ; ustawiamy POKEY-a do
 sta $d20f     ; transmisji (zapisu)
 lda #$10      ; przerwanie zapisu
 sta $d20e
 lda #$31      ; wysyłamy pierwszy bajt do
 sta $d20d     ; stacji
 sta cksum     ; zliczamy sumę kontrolną
rts rts

* przerwanie zapisu danych *

irq2 cmp #$20  ; czy to aby na pewno do mnie?
 bne irq3      ; do przerwania koca transmisji
 lsr @         ; ustawiamy na nowo przerwanie
 sta $d20e     ; do zapisu
 inc lindex
 ldx lindex
 cpx #4        ; czy nadal wysyłamy komendę?
 bcs oi1
 lda dcb,x
 sta $d20d     ; wysyłamy komendę
 clc           ; zliczamy sumę
 adc cksum
 adc #0
 sta cksum
 bcc irqend    ; kończymy przerwanie (bcc=jmp)
oi1 bne oi2
 lda cksum     ; wysyłamy sumę kontrolną
 sta $d20d
irqend pla     ; kończymy przerwanie
 tax
 pla
 rti
oi2 lsr @      ; ustawiamy przerwanie koca
 sta $d20e     ; transmisji
 bne irqend    ; (bne=jmp)

* przerwanie końca transmisji *

irq3 lda #$13  ; ustawiamy POKEY-a do
 sta $d20f     ; transmisji (odczytu)
 sta $d20a     ; to nie jest ustawianie generatora liczb losowych :-)
               ; W trybie zapisu ten rejestr pełni funkcję
               ; resetu złącza szeregowego. Jeśli nastąpił
               ; błąd transmisji to musimy złącze resetować,
               ; a skoro tak, to dlaczego nie robić tego
               ; po prostu zawsze? P.S. wsadzana wartość
               ; nie mają znaczenia (podobnie jak przy $d01e).

 lda #$20      ; przerwanie odczytu
 sta $d20e
 lda #$3c      ; informujemy stację, że coś
 sta $d303     ; będziemy od niej odbierać
 lda #$fe      ; zerowanie licznika
 sta stcnt     ; odbieranych bajtów
 lda #0        ; i sumy kontrolnej
 sta cksum
 beq irqend    ; (beq=jmp)

* główne przerwanie *

irq pha
 txa
 pha
 ldx #0
 lda $d20e     ; sprawdzamy jakie nastąpiło przerwanie (bity przy odbiorze są
               ; negacją tych wsadzanych do tej komórki)
 stx $d20e     ; zerowanie rejestru, aby mógł wskazywać kolejne przerwania
 and #$30
 cmp #$10
 bne irq2

* przerwanie odczytu *

 asl @         ; ustawiamy na nowo przerwanie
 sta $d20e
 lda $d20f     ; pobieramy status błędu
 sta $d20a     ; kasujemy status błędu
 bpl error     ; skasowany bit najwyższy i 6-ty
 and #$20      ; informują, że nastąpił błąd
 beq error
 ldx stcnt     ; czy pobieramy teraz dane
 bmi getsum    ; sektora? (X=0-127)
 lda $d20d     ; pobieramy bajt
 sta bufor,x   ; i do bufora
 clc           ; zliczmy sumę kontrolną
 adc cksum
 adc #0
 sta cksum
 inc stcnt     ; powiększamy ilość
 pla           ; odczytanych bajtów
 tax
 pla
 rti
getsum cpx #$80; czy przesyłana jest
 beq ii1       ; suma kontrolna?
 inc stcnt     ; jak nie, to powiększ ilość
 lda $d20d     ; przeczytanych bajtów i
 cmp #$41      ; sprawdź, czy bajt statusu
 beq endirq    ; wysłanego przez stację
 cmp #$43      ; wskazuje, że wszystko O.K.
 beq endirq
error jsr del  ; jeśli nastąpił błąd, to
 jsr set       ; odczytaj sektor jeszcze raz
endirq pla     ; koniec przerwania
 tax
 pla
 rti
ii1 lda $d20d  ; sprawdzamy sumę kontrolną
 sbc cksum     ; jeśli wszystko O.K., to dane
 bne error     ; z bufora przepisujemy

* loader właściwy *

 tax zerujemy  ; licznik odebranych bajtów
 stx lindex
 lda bufor+$7e ; który następny
 sta dcb+2     ; sektor odczytać?
 lda bufor+$7d
 and #3
 sta dcb+3
 ora dcb+2     ; jeśli zerowy, to znak, że to
 beq l7        ; koniec pliku
 lda #$34      ; jeśli jednak będziemy jeszcze
 sta $d303     ; odczytywać dane, to
               ; przygotowujemy stację na zapis komendy
               ; (czas trwania przepisywania danych będzie
               ; tą pętlą służyć wyczekaniu, aż stacja
               ; załapie o co chodzi).
l7 sta l8+1    ; l8+1 to bajt, który mówi nam
               ; czy będziemy jeszcze odczytywać sektory

 tya           ; zachowujemy dodatkowo Y
 pha
l1 lda bufor,x
 ldy xdone     ; jaki jest stan loadera
 beq l2        ; 0 = odczytujemy dane
 sta adr-1,y   ; nie zero? to znak, że jest
               ; to adres bloku
 lda <rts      ; po każdym bloku jest robiony
 sta $2e2      ; jmp ($2e2). Jeżeli żaden
 lda >rts      ; adres nie był tam ustawiony
 sta $2e3      ; to procesor napotka RTS
 inc xdone     ; zwiększ stan loadera
 cpy #2        ; czy przesłany został cały
 bne l4        ; adres początku bloku?
 lda adr       ; sprawdź, czy nie wynosi on
 and adr+1     ; $ffff, jeśli tak, to znaczy, że
 eor #$ff      ; jest to tylko informacja, że
 bne l3        ; ten plik jest binarny
 lda #1        ; przeczytaj adres jeszcze raz
 bne l6        ; (bne=jmp)
l4 tya
 sec
 sbc #4        ; sprawdź, czy przeczytany już
 bne l3        ; został cały nagłówek
l6 sta xdone   ; jeśli tak, to odczytujemy
 jmp l3        ; dane bloku

l2 sta (adr),y ; umieszczamy bajt
 lda adr       ; sprawdzamy, czy to już
 cmp end       ; cały blok
 lda adr+1
 sbc end+1
 bcc l5
 inc xdone     ; jeśli tak, to przystępujemy
               ; na nowo do czytania nagłówka
 stx cksum X   ; może nam się przydać
 jsr init      ; po przeczytaniu całego bloku
               ; robimy skok po $2e2. Standardowo ustawiany jest tam
               ; skok pod rozkaz RTS.

 ldx cksum     ; bierzemy X z powrotem
l5 inc adr     ; następny bajt wsadzimy w
 bne l3        ; następną komórkę
 inc adr+1
l3 inx
 cpx bufor+$7f ; sprawdzamy, czy tylko tyle bajtów w tym sektorze należy do pliku
 bcc l1        ; jeśli nie, to odczytujemy następny
 pla           ; pobieramy Y z powrotem
 tay
l8 lda #10     ; jeśli to był ostatni sektor pliku, to tutaj jest #0
 beq *+5       ; a wówczas...
 jmp error+3   ; odczyt następnego sektora
 jmp ($2e0)    ; uruchamiamy program

 end
</pre>

<p>
 No i tak to wygląda. Może na początku
jest to nieco skomplikowane, ale po bliższym
przyjrzeniu się, każdy powienien wszystko
zrozumieć. Aby było łatwiej, wyjaśnię może
dokładniej procedurę odczytu i zapisu:
<br><br>

 Proces zapisu bajtu do stacji
polega na tym, że bajt wysyłany wsadzamy
do komórki $d20d, a przerwanie zapisu
następuje PO wysłaniu tego bajtu do stacji.
<br>

Tak więc pierwszy bajt wsadzamy poza
przerwaniem, drugi w przerwaniu
informującym, że pierwszy bajt został
wysłany itd. W przerwaniu informującym, że
wysłana została suma kontrolna (która
zawsze jest wysyłana na końcu wysyłanego
bloku danych) ustawiamy jako następne
przerwanie zakończenia transmisji (w
domyśle zapisu, gdyż tylko wtedy to
przerwanie jest wykorzystywane).
<br><br>

 Proces odczytu jest trochę prostszy.
Przerwanie odczytu wywoływane jest tutaj
zawsze po odczytaniu bajtu ze stacji. W
przerwaniu właśnie ten bajt odczytujemy z
komórki $d20d. Po odczytaniu wszystkich
bajtów odczytujemy sumę kontrolną. Należy
przy tym uważać gdyż bajty statusu stacji,
wysyłane przez nią dla potwierdzenia, że
dostała i zrozumiała komendę, nie są do
sumy kontrolnej wliczane.
</p>

<p>

 A teraz po kolei w punktach proces
odczytu sektora:
<br><br>

1) Wysłanie 4 bajtów komendy + suma.
<br><br>

2) Natychmiast po tym, stacja wysyła nam
bajt $41, który informuje nas, że stacja
zrozumiała komendę.
<br><br>

3) Teraz następuje chwila przerwy. Stacja
musi zakręcić dyskiem i odczytać sektor.
<br><br>

4) Jeśli sektor na dysku był
prawidłowy, stacja wysyła nam bajt $43
który informuje nas, że wszystko O.K. i
zaraz nam wyśle dane.
<br><br>

5) Odbieramy 128+1 (256+1 lub 512+1
-zależnie gęstości dyskietki) bajtów danych
sektora z sumą kontrolną.
<br><br>

6) Koniec transmisji sektora.
<br><br>

 A teraz dla aktywnych zapis:
<br><br>

1) 4+1 bajtów -komenda + suma.
<br><br>

2) Natychmiast po tym stacja wysyła nam
$41, że zrozumiała komendę.
<br><br>

3) Wysyłamy 128+1 (256+1 lub 512+1
-zależnie od gęstości dyskietki) bajtów
danych sektora z sumą kontrolną. Ponieważ
stacja jest przygotowana na to, nie musimy
dawać takiej długiej pętli po umieszczeniu
#$34 w komórce $d303.
<br><br>

4) Teraz następuje chwila przerwy. Stacja
zakręci dyskiem i zapisze sektor.
<br><br>

5) Odbieramy bajt $43, który oznacza,
że sektor został prawidłowo odebrany i
zapisany.
<br><br>

6) Koniec transmisji.
<br><br>

 I co? Nadal jest to takie trudne?
<br><br>

 Jak zapewne zauważyliście w Energy
#1 jest więcej niż jeden IRQ-loader. Drugi
uruchamiany jest po intrze podczas
ładowania całego magazynu. 
</p>

<p>
Jego cechą
charakterystyczną jest to, że oprócz
muzyczki na dwóch kanałach, odgrywane są
tam na dwóch kanałach sample. Wbrew
pozorom jest to bardzo prymitywny efekt.
</p>

<p>
Zauważcie bowiem, że do operacji
zapisu-odczytu używane są faktycznie
generatory 3 i 4 POKEY-a, ale tylko i
wyłącznie dla ustalenia częstotliwości
transmisji. Ich głośność do tego nic nie
wnosi, a tylko tyle potrzeba, aby sample
mogły grać. 
</p>

<p>
Dodatkowo mamy jeszcze jedno
ułatwienie. Po wsadzeniu wartości $34 do
komórki $d303 nie musimy robić takiej
długiej pętli oczekując na to, aż stacja
załapie, że chcemy do niej coś wysłać. Po
prostu w tym czasie wywołujemy player.
Drobne problemy nastręczyć może
procedura odgrywania sampli. Nie możemy
jej przerywać na nazbyt długo, bo sample
zaczną źle brzmieć, a procedura
przepisująca bufor do pamięci trwa
naprawdę sporo.
</p>

<p>
 Rozwiązanie jest proste.
Ta procedura nie będzie znajdować się w
przerwaniu, ale w normalnym programie, do
którego skaczemy po ustawieniu się
znacznika, że cały sektor został
przeczytany, a w jej środek wsadzamy
drugą procedurę odgrywania sampli. Całość
działa w sposób następujący.
</p>

<p>
 Przepisanie jednego bajtu z bufora, odegranie sampla,
przepisanie bajtu z bufora, odegranie
sampla itd.
</p>

<p>
 Trzecim typem loadera użytym w
Energy #1 jest loader ładujący artykuły.
Wbrew pozorom nie jest on identyczny z
loaderem przedstawionym w tym artykule.
Ktoś spostrzegawczy zauważył zapewne, że
podczas działania tego loadera na ekranie
znajduje się logos w pięciu kolorach. A
skoro tych kolorów jest pięć, to znaczy, że
jest na fontach. A skoro ten logos jest
duży, to znaczy, że są 2 generatory
znaków. A skoro są 2 generatory, to
znaczy, że gdzieś w środku jest przerwanie
NMI. A skoro jest przerwanie NMI, to nie
może być przerwań IRQ, gdyż mają one
tę właściwość, że mogą opóźnić odebranie
NMI. A zatem całość musi być poza
przerwaniami IRQ.
</p>

<p>
 Niby niemożliwe, ale
zauważmy, że tak naprawdę, to przerwania
potrzebne są nam tylko do tego, aby
dowiedzieć się kiedy odebrać następny bajt
ze stacji, albo go do niej wysłać. Tego zaś
możemy dowiedzieć się z komórki $d20e. Bity
w niej są bowiem kasowane właśnie przy
wystąpieniu danego przerwania. Loader
jest dość podobny do tego
przedstawionego tutaj. Różnice polegają na
tym, że nie ma rozkazu CLI, a procedury w
przerwaniach są przeniesione do głównego
programu i dodana jest procedurka
śledząca komórkę $d20e i w zależności od
niej skacząca do odpowiednich procedur.
</p>

<p>
 I to by było na tyle, jeśli chodzi o
własne procedury obsługi stacji. W
następnym numerze postaramy się
rozszerzyć ten temat o procedury obsługi
w różnych systemach turbo oraz (jeśli uda
nam się namówić na to Foxa) procedury dla
stacji Karin.
</p>

<p>
 Jaskier/Taquart
</p>

</p>
</p>
</p>
</p>

</html>

<hr>

## Kilka słów o formacie KOALI

<html>

<div style="float: right">
<img src="../gfx/dracon.jpg" alt="dracon" width="80" height="117"><br>autor: dracon
<br>
</div>

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

<p align=right>
Specjalnie dla Was "produkował się"...<br>
-Dracon-
</p>

</html>
