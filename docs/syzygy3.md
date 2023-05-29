#

## Lekcja assemblera

Charlie


Na początek parę słów tytułem wstępu. Pierwsza lekcja ukazała się podobno w pierwszym numerze Syzygy. 

Nie uważam się za jakiś autorytet w tej dziedzinie jednak zostałem poproszony przez redakcję o poprowadzenie tej rubryki. 

Mam nadzieję, że komuś się to moje kwaszenie przyda. Wszelkie źródłówki będą napisane w formacie **Quick Assemblera** i dołączone do zina w postaci plików z rozszerzeniem "ASM". 

Rubrykę tę powinny czytać osoby mające już jakieś pojęcie o assemblerze, dla początkujących może to być zupełna abstrakcja.

___- INTEGER -___

Istnieje wiele sposobów reprezentacji liczb we wnętrzu komputera. Chciałbym jednak zająć się bliżej bardzo popularnym formatem zapisu dwubajtowych liczb całkowitych o nazwie **integer**. Jeżeli ktoś zajmował się programowaniem na PC, na pewno musiał się z nim zetknąć. Występuje on zarówno we wszelkich kompilatorach języka Pascal, C, a także w assemblerze.

Jak już wspomniałem, liczba w formacie **integer** reprezentowana jest przez 16 bitów, z czego najstarszy określa znak (ustawiony oznacza liczbę ujemną). Tak więc w tej postaci możemy zapisać liczbę całkowitą z przedziału domkniętego <-32768; +32767>.

Postarajmy się teraz zaimplementować operacje arytmetyczne dla formatu **int**.:


___1. Dodawanie i odejmowanie.___

Z tym nie ma żadnego problemu. Trzeba tylko pamiętać o znaczniku C procesora.

```
    c := a + b

iadd    clc
        lda     inta
        adc     intb
        sta     intc
        lda     inta+1
        adc     intb+1
        sta     intc+1
        rts
```

```
    c := a - b

isub    sec
        lda     inta
        sbc     intb
        sta     intc
        lda     inta+1
        sbc     intb+1
        sta     intc+1
        rts
```

Uwidacznia się tu wielka zaleta takiego zapisu liczb całkowitych. Gdybyśmy znak zapisali w osobnym bajcie, wówczas musielibyśmy rozpatrywać możliwe przypadki: czy która z liczb jest ujemna, która jest większa itd. W oparciu o odejmowanie możemy zapisać procedurę negacji liczby. W końcu jest to odjęcie jej od zera. Poprzez negację rozumiem tu zmianę znaku liczby...

```
    c := -c

ineg    sec             ; -c := 0 - c
        lda     #0
        sbc     intc
        sta     intc
        lda     #0
        sbc     intc+1
        sta     intc+1
        rts
```

Jeżeli mamy procedurę negującą, możemy zapisać wartość bezwzględną:

```
    c := abs( c )

iabs    lda     intc+1  ; jeśli ujemna,
        bmi     ineg    ; to zmień znak
        rts
```

W prosty sposób można również zapisać funkcję signum, zwracając w akumulatorze znak liczby. Jest ona zupełnie zbyteczna, ale dla zasady należy ją zapisać:

```
    Acc := sgn( c )

isgn    lda     intc+1
        bpl     isg1
        lda     #256-1  ; liczba ujemna
        rts

isg1    beq     isg2
isg3    lda     #1      ;liczba dodatnia
        rts
isg2    lda     intc
        bne     isg3
        rts             ; zero
```

Funkcja ta przyjmuje trzy wartości:

    -1 - oznacza liczbę ujemną,

    0 - oznacza zero,

    1 - oznacza liczbę dodatnią.

Procedury te są bardzo proste, dlatego jeżeli zależy nam na prędkości, operacje należy umieścić bezpośredni w programie. Przykłady te ilustrują tylko, jak te procedury powinny wyglądać...

Warto podkreślić, że nie zmieniają one zawartości rejestrów int i intb...

___2. Mnożenie i dzielenie.___

Tutaj zaczynają się problemy. Można te operacje zaimplementować na wiele sposobów, ale należy pamiętać o następujących rzeczach:

- należy ustalić znak wyniku,
- w przypadku mnożenia należy sprawdzić, czy jeden z czynników nie jest zerem, wówczas wynik również jest zerowy;
- podobnie w przypadku dzielenia, jednak jeśli dzielnik jest równy zero, wówczas występuje błąd ("Cholero nie dziel przez zero").

Na początek proponuję napisać procedurę, która zadba o znak wynik i sprawdzi czy która z liczb jest równa zero. Aby uzyskać znak wyniku, wystarczy zEORować znaki czynników.

```
isig    lda     #0
        sta     intc    ; wyzerowanie
        sta     intc+1  ; wyniku
        lda     inta
        ora     inta+1  ; czy a = 0?
        bne     sg0
        sta     intb    ; 0 mod b = 0!
        sta     intb+1
sg1     pla             ; wynik zerowy,
        pla             ; wyjdź
        rts
sg0     lda     intb
        ora     intb+1  ; czy b = 0?
        beq     sg1
        lda     inta+1
        eor     intb+1
        sta     ints    ; znak wyniku
        lda     inta+1  ; a := abs( a )
        bpl     sg2
        sec
        lda     #0
        sbc     inta
        sta     inta
        lda     #0
        sbc     inta+1
        sta     inta+1
sg2     lda     intb+1  ; b := abs( b )
        bpl     sg3
        sec
        lda     #0
        sbc     intb
        sta     intb
        lda     #0
        sbc     intb+1
        sta     intb+1
sg3     rts             ; wyjście do nadrzędnej ;procedury...
```

Należy się tutaj parę wyjaśnień. Dla uproszczenia przyjmijmy, że dowolna liczba podzielona przez zero, daje w rezultacie zero. Jest to sprzeczne, ale człowiek myślący, przez zero i tak dzielił nie będzie. To uproszczenie pozwoli na to, że procedury tej będziemy mogli używać zarówno podczas mnożenia, ja i dzielenia. Jeśli któraś z liczb jest równa zero, wówczas procedura powraca do programu głównego z wyzerowanym wynikiem. Ponadto dba ona o znak wyniku, zapamiętując go w bajcie ints, następnie oblicza wartości bezwzględne z licz a i b, gdyż jest to konieczne, aby procedury mnożenia i dzielenia działały poprawnie.

Teraz możemy zająć się implementacją mnożenia i dzielenia. Przykładowy algorytm mnożenia mógłby wyglądać następująco:

    c := 0 (wyzerowanie wyniku)

    sprawdź czy a lub b = 0, jeśli tak, to skocz do punktu 10.

    zapamiętaj znak wyniku,

    a := abs(a), b := abs(b),

    c := c + a,

    b := b - 1,

    jeśli b > 0 skocz do punktu 5.

    jeśli znak wyniku jest dodatni, skocz do punktu 10.

    c := -c (zanegowanie wyniku),

    powróć do programu głównego.

Implementacja tego w assemblerze byłaby bardzo prosta, tym bardziej, że punkty 1-4 odwala już nasza procedura isig. Jednak algorytm ten jest zbyt wolny... Nie zawsze prosty, znaczy szybki. Należy poszukać bardziej efektywnej metody.

Zapewne każdy kto chodził do podstawówki pamięta właściwości mnożenia dwóch liczb. Jest przemienne, a poza tym każdy czynnik można rozłożyć na elementarne składniki, np.

	37 * 47 = 37 * ( 40 + 7 ) = 37 * 40 + 37 * 7

A gdyby ten drugi czynnik rozkładać na kolejne potęgi dwójki?

	47 = 25 + 23 + 22 + 21 + 20

Mnożenie przez potęgi dwójki można naturalnie zastąpić przesuwaniem bitów. Nasza procedura mnożenia może teraz wyglądać następująco:

```
    c := a * b

imul    jsr     isig    ; zadbaj o znak
        ldx     #0      ; wyniku
        ldy     #0
_ml1    lsr     intb+1  ; przesuwanie
        ror     intb    ; bitó w prawo
        bcc     _ml2    ; czy pomnożyć
        txa             ; przez 2n?
        clc
        adc     inta    ; dodanie do
        tax             ; wyniku
        tya
        adc     inta+1
        tay
_ml2    lda     intb    ; czy jeszcze
        ora     intb+1  ; trzeba coś
        beq     _ml3    ; dodać?
        asl     inta    ; a := a * 2
        rol     inta+1
        jmp     _ml1
_ml3    stx     intc    ; zapamiętaj
        sty     intc+1  ; wynik
        lda     ints    ; jeśli znak "-"
        bmi     ineg    ; to wynik musi
        rts             ; być ujemny!
```

Teraz nasza procedura jest już całkiem szybka. Jednak należy się parę wyjaśnień. 

Liczbę b przesuwamy w prawo. Jest to równoznaczne z dzieleniem przez 2, zaś resztę z tego dzielenia (0 lub 1) znajdziemy w znaczniku C procesora. 

A po co to w ogóle robimy? Ano po to, żeby zbadać, czy w zapisie dwójkowym bit o danym numerze jest zapalony. 

Równorzędnie z dzieleniem b, mnożymy a przez 2. Jeśli n-ty bit liczby b jest zapalony, wówczas do wyniku dodajemy liczbę a pomnożoną przez 2n, np.

	10 * 6 = 10 * ( 0 * 20 + 1 * 21 + 1 * 22) = 10 * 21 + 10 * 22 = 60

Czas zająć się dzieleniem całkowitym. Nie ma ono takich samych właściwości jak mnożenie, więc jego implementacja oparta na przesuwaniu bitów nie jest taka prosta. 

Poza tym dzielenie jest znacznie mniej razy używane, więc nie musimy się troszczyć w jego przypadku o prędkość. 

Wystarczy, żeby "chodziło i można było obliczyć również resztę z dzielenia.

___Przykładowy algorytm:___

    c := 0 (wyzerowanie wyniku)

    sprawdź czy a lub b = 0, jeśli tak, to skocz do punktu 11.

    zapamiętaj znak wyniku,

    a := abs(a), b := abs(b),

    a := a - b,

    jeśli a < 0 skocz do punktu 9.

    c := c + 1,

    skocz do punktu 5.

    jeśli znak wyniku jest dodatni, skocz do punktu 11.

    c := -c (zanegowanie wyniku),

    powróć do programu głównego.

Przypominam, iż w celu uproszczenia nie uwzględniamy błędu dzielenia przez 0. Darujmy sobie idiotoodporność...

___A oto implementacja w assemblerze:___

```
    c := a div b

idiv    jsr     isig    ; zadbaj o znak
        ldx     inta
        ldy     inta+1
_dv1    sec
        txa
        sbc     intb    ; a := a - b
        tax
        tya
        sbc     intb+1
        tay
        bcc     _dv2
        inc     intc    ; c := c + 1
        bne     _dv1
        inc     intc+1
        bne     _dv1    ; (jmp)
_dv2    stx     inta
        sty     inta+1
        lda     ints    ; zadbaj o znak
        bmi     ineg
        rts
```

Prosto i zwięźle. Przy okazji możemy napisać procedurę obliczającą resztę z dzielenia.

```
    c := a mod b

imod    lda     inta+1  ; zapamiętaj
        php             ; znak a
        jsr     idiv    ; podziel
        jsr     iadd    ; dodaj
        plp             ; jeśli znak "-"
        bmi     ineg    ; to zaneguj
        rts             ; wynik...
```

Oczywiście, jest ona zupełnie zbyteczna, pokazuje tylko jak to zrobić. Po wywołaniu procedury dzielenia wystarczy wywołać dodawanie, a wynikowi nadać znak dzielnej...

Dzielenie tym sposobem jest bardzo wolne, jednak spełnia swoje zadanie. Nawet jeżeli ktoś napisałby superszybką procedurę dzielenia, to i tak mnożenie jest szybsze (a przecież dzielenie to mnożenie przez odwrotność, więc przy obliczeniach stałopozycyjnych można zastosować tablicę i mnożyć...).
