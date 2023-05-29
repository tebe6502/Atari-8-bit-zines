#

## NeoTracker - co i jak?

Praca konkursowa


Był sobie magazyn dyskowy. Nazywał się **Serious Magazine**. Gdzieś w numerze jedenastym, Wielce Szanowna Redakcja tegoż Magazynu ogłosiła konkurs... Temat dowolny, forma dowolna, ma być o Atari i... najlepsze z najlepszych.

(to nie redakcja ogłosiła konkurs, tylko ja, **Zenon/DIAL**, a **Jager** maczał w tym swoje palce)

W czym więc problem? Hehe... hmmm... ee... no... tego... nie miałem żadnego pomysłu :( ... A Redaktor Naczelny, dobry przyjaciel nas wszystkich, a mój szczególnie, napisał do mnie: "No a konkurs w Seriousie? chyba tego nie odpuścisz?". Nie mogłem więc zawieść przyjaciela. Całe wakacje myślałem, co by tu przygotować. Może jakiś modułek, ale z drugiej strony... mam tylko jeden, niezbyt dobry, no i ma pójść na msx-compo na party... A po party był już kompletny dół, bo wena mnie kompletnie opuściła. Ale, ale...

Z nieco innej beczki. Parę razy rozmawialiśmy z **Pinokiem** o tym, jaka ta **Inertia** i jaki ten **ProTracker** jest be i w ogóle. A bo cośtam mu dłuższe modułki się sypią. A bo nie obsługuje podkatalogów i w dodatku tylko kilka modułów na jednym dysku. A on ma HDD, więc go to boli. I ja go rozumiem... A chciałem coś takiego napisać. Ale był jeden problem: skąd taki nieuk jak ja może wiedzieć, jak odtwarzać sample z różną częstotliwością? Aż wstyd się przyznać, jakie absurdalne pomysły przychodziły mi do głowy, zanim... nadszedł TEN dzień: 12.08.07d2...

W nocy z soboty na niedzielę nie mogłem zasnąć i mniej więcej o wpół do trzeciej, po dwóch godzinach przewracania się z boku na bok... Wpadłem na tak prostą rzecz, że teraz wstyd się przyznać, że kończąc 16 lat o niej nie wiedziałem. O sssooo choozzziii? ;)

Przypomniał mi się wtedy artykuł **Krógera** "Siedemnastobitowa arytmetyka" a dokładniej... ułamki binarne. Boże na wysokim niebie, czemu ja na to wcześniej nie wpadłem?! Przecież żeby odtwarzać sample z różną częstotliwością, wystarczy zwiększać adres aktualnie odtwarzanej próbki nie co 1, tylko o mniejsze lub większe wartości, często niecałkowite, a właściwa częstotliwość odtwarzania pozostaje stała! No... dobra, to wiedziałem już nieco wcześniej, aż taki głupi nie jestem. Tylko że we łbie mi się nie mieściło, jak można dodawać ułamki z taką szybkością, żeby częstotliwość odtwarzania nie powodowała odruchu zwanego przez **X-Ray**'a (gtx!) "zamykaniem uszu". Jak by to ujęły osoby pokroju koleżanek mojej siostry: "Obciach po maksie!"

Kiedy tylko się obudziłem, zacząłem robić tablice częstotliwości, pchełkę w **QA**, żeby potwierdzić oczywistą hipotezę i kiedy udało mi się odpalić melodyjkę na samplu w 15kHz, to ciśnienie tak mi podskoczyło, że pisałem na pełnych obrotach przez dwa tygodnie aż wreszcie skończyłem. Jednak zanim skończyłem, miałem trochę przygód. Od początku:

Następnego dnia miałem już kilka procek, ekran i przede wszystkim nazwę: **NEOTRACKER**. Ponieważ poetą nie jestem, więc na nic lepszego nie było mnie stać. Zmysł estetyczny też mam wątły (ale mam! ;)) i dlatego program wygląda, tak jak wygląda. Spieszyło mi się, bo w tzw. "międzyczasie" wpadłem na kolejny genialny pomysł... Oto jest moja praca na konkurs najpoczytniejszego maga na Atari! Ale wtedy dostałem "spida"... ;)

Dnia 15.08.07d2, czyli, jak to się mówi, w środę wieczorem, nastąpiło pierwsze odpalenie modułku w **NeoTrackerze**. MASAKRA - częstotliwość co pięć linii... 3.1kHz. Gratulacje. Ale się nie poddałem. Cały tydzień ciężko pracowałem, aby przyspieszyć ją przynajmniej do 11kHz, bo kiedy postawiłem pierwsze LDA w kodzie Neo, zawziąłem się, że będzie to cacuszko, więc jakbym nie przebił częstotliwości odtwarzania z **Inertii**, to chyba bym się powiesił. Tyle roboty i taka plama? Po kolei więc wywalam wszystkie śmieci: adresowanie pośrednie, jakieś liczniki, w końcu całość ląduje na stronie zerowej, kontrolę naciśnięcia spacji dodałem do przerwania taktującego (czyli do czegoś, co w "normalnych" atarowskich tracker-ach nazywa się "player-em co ramkę"), duża część danych jest pobierana w trybie natychmiastowym (niech żyje assembler i automodyfikacja!) ...

Kiedy doszedłem do 10.95kHz, ciągle byłem pewien, że można więcej. Ale nie miałem pomysłów. Odpaliłem **Inertię** wcisnąłem SELECT+RESET, potem RETURN. szukam playerka sampli w kodzie. Jest. Be. Co zobaczyłem? Dokładnie to samo, co u mnie, tylko gorzej, bo w Neo taktowanie już było na przerwaniu, a IP po prostu odlicza do $D8, po czym wywołuje "ramkę". Strata czasu. __Profi__ widać dał się zwieść nie do końca prawdziwej teorii, że odłączenie przerwań przyspiesza działanie programu. Umiejętne wykorzystanie przerwania pozwala zaoszczędzić sporo czasu na odliczaniu. Wystarczy podmienić zawartość wektora NMIVEC...

W niedzielę wieczorem przyszło kolejne olśnienie. Zaraz! Po co mam porównywać adres próbki z adresem końca sampla, skoro wystarczy go tak umieścić, aby ostatni bajt był pod $7FFF, a przekroczenie przez starszy bajt adresu wartości $7F spowoduje ustawienie bitu N rejestru znaczników. A więc... jedno BPL i kłopot z głowy! Błogosławiony niech będzie ten, kto ustawił pamięć dodatkową w obszarze $4000-$7FFF! Chociaż... Gdyby była w $8000-$BFFF, to można by zastosować podobny trik. Jak? Zgadnijcie sami! :)

Ostatecznie na początku następnego tygodnia procedura odtwarzająca była już kompletna, a wyglądała tak: (listing dla X-Assemblera 2.5)

```
  opt   h-
  org   $00            ;cykli  suma

 songpsl lda   #0         2    2
 t1bnk   equ   *-1
         sta   ^31        4    6
         lda   #0         2    8
 t1ind   equ   *-1
         adc   #0         2    10
 t1frq_l equ   *-1
         sta   z:t1ind    3    13
         lda   z:t1iadr   3    16
         adc   #0         2    18
 t1frq_h equ   *-1
         sta   z:t1iadr   3    21
         bcc   play1      3/4  24/25
         inc   z:t1iadr+1 5    29
         bpl   play1      3/4  32/33
         lda   #0         2    34
 t1rep_l equ   *-1
         sta   z:t1iadr   3    37
         lda   #0         2    39
 t1rep_h equ   *-1
         sta   z:t1iadr+1 3    42
         jmp   spslt2     3    45
 play1   ldx   $4000      4    29/37
 t1iadr  equ   *-2
         lda   $d800,x    4    33/41
 t1vol_  equ   *-1
         sta   $d600      4    37/45
 t1pflg  equ   *-1
```

I jeszcze trzy razy dla kolejnych trzech kanałów (każdy zaczyna się od etykiety **spslt#**, gdzie **#** to numer kanału) to samo, oraz na samym końcu **jmp songpsl** zajmujące 3 cykle.

Algorytm, z którego wynika treść tej pętelki jest opisany w innym artku, tutaj ograniczę się do opisu samej procki.

Kolejne etykiety oznaczają:

|  Etykieta  |                      Opis                           |
|------------|-----------------------------------------------------|
|**songpsl** |początek pętli odtwarzającej sample w oknie song <br> (dla paternów i pojedynczych sampli są osobne procki)|
|**t1bnk**   |kod banku na danej ścieżce                           |
| **t1ind**  | ułamkowa część adresu                              |
| **t1frq_l/h**| okres dźwięku względem częstotliwości bazowej     |
| **t1rep_l/h**| adres początku pętli                              |
| **spslt2**| początek fragmentu obsługującego kolejną ścieżkę   |
| **play1**| tu zaczyna się właściwa "odtwarzarka" ;)           |
| **t1iadr**| adres próbki                                       |
| **t1ivol_**| adres tablicy głośności (od $D800 zaczyna się tablica dla vol=$00 <br> i tak co stronę aż do $F000, gdzie jest tablica dla vol=$40)|
| **t1pflg**| jeżeli ścieżka jest wyłączona, to tutaj zamiast $d6 program wpisuje $FF, <br> żeby na tej ścieżce nic nie grało, a jednocześnie żeby nie tracić czasu <br> na sprawdzanie innych zmiennych (ma grać, czy nie?)|

W ostatniej kolumnie z prawej strony cykle są sumowane, ostateczne wartości po zakończeniu działania tej części pętli są odpowiednio wyróżnione. Widać więc, że pojedynczy kanał jest obsługiwany w czasie 37 lub 45 cykli, przy czym ta druga wartość występuje średnio raz na jakieś 190 wywołań. Zależy to od wysokości sampli na poszczególnych kanałach i od pozycji początku pętli. Liczby te są wyraźnie mniejsze niż w **Inertii**, mniejsza jest też różnica między nimi, dzięki czemu częstotliwość odtwarzania jest większa i bardziej stabilna. A ile wynosi? W sumie procedura zajmuje 4*37+3= 155 cykli. Raz na owo statystyczne 190 może mieć 4*45+3= 183 cykle. Zegar procesora ma w ciągu sekundy 1778400 cykle, tak więc częstotliwość powtarzania się naszej pętli to około...

	190*1778400/(189*151+183) Hz

(mam nadzieję, że sposób wyprowadzenia wzoru jest dla wszystkich jasny)

czyli... uwaga, uwaga...

	11764 Hz

A więc możemy przyjąć, że jest to 11.7 kHz. W tym momencie mnie zatkało, bo na potrzeby tego opisu przeliczałem cykle i częstotliwość jeszcze raz i okazało się, że wcześniej popełniłem błąd, uznając, że częstotliwość wynosi 11.3 kHz. Szok. Ale bardzo miły :)

To tyle odnośnie samego odtwarzania sampli. Pozostałe "sztuczki", których opis wedle regulaminu jest "wskazany", nie są już tak spektakularne.

Procedura play_song odpowiedzialna za odtwarzanie muzyki przenosi pętlę odtwarzającą na stronę zerową, odłącza ROM i przerwania, inicjuje zmienne, ustawia wektor przerwań NMI na adres początku playera i włącza przerwanie VBLANK.

Player jest wywoływany na przerwaniu VBLANK, bezpośrednio z wektora NMIVEC. Na samym początku procka zapamiętuje zawartość akumulatora. Następnie sprawdza, czy wciśnięto spację, co oznacza że należy przerwać odgrywanie. Następuje wtedy przejście do procedury kończącej odgrywanie - zdejmuje ona ze stosu wartość akumulatora oraz 3 bajty dla RTI, przywraca poprzednią zawartość strony zerowej, włącza ROM i przerwania oraz resetuje klawiaturę.

Jeżeli spacja nie została wciśnięta, to w dalszej części zmniejszany jest licznik kontrolujący tempo odtwarzania muzyki, jeżeli osiągnie zero, to jest on ustawiany na aktualną wartość tempa i rozpoczyna się dekodowanie paternów, które nie jest jakoś szczególnie interesujące pod względem "tricków". Charakterystyczne jest tylko to, że jeżeli nastąpiło przejście do kolejnej linii w paternach (po każdym wyzerowaniu licznika), to na końcu procedury przerwania playera ze stosu zdejmowane są cztery bajty (akumulator oraz F i PC-1 dla RTI) i następuje skok do początku procedury odtwarzającej sample (songpsl = $00). Dlaczego? Ano dlatego, że wywołanie przerwania mogło wystąpić np. w połowie zwiększania adresów na którymś kanale, a w czasie tego przerwania na tym kanale pojawił się nowy dźwięk i jego adres został umieszczony w procedurze. Tak więc końcowym efektem braku takiego zabezpieczenia będzie w najlepszym wypadku "pykanie" w głośnikach. W najgorszym - mogłyby pojawić się "zgrzyty". Skąd wiem? Gdybym tego nie zaobserwował, to zabezpieczenia tego by nie było. :)

Normalne wyjście z procedury przerwania (PLA, RTI) następuje tylko jeśli licznik taktujący odtwarzanie nie osiągnął jeszcze zera.

Wszystkie te cuda napisałem sam, za wyjątkiem procedury wykrywającej XMS autorstwa **Foxa/TQA** (**Syzygy #7**). Moja jakoś nie chciała działać na kompach z pamięcią poniżej 1MB... ;) a brakło mi czasu na szukanie pluskwy.

I to już chyba wszystkie szczegóły techniczne dotyczące nowinek obecnych w **NeoTrackerze**.

Wiecie już chyba, że staliście się ofiarami mojej nudy i spóźnionego geniuszu? ;) ... hmm... Do programu miał być pierwotnie dołączony jeszcze program **NeoPlayer** do odtwarzania modułów .NEO i .MOD oraz pchełka do konwersji MODów na format **NeoTrackera**. Niestety, za słabo się starałem. W końcu zaczęła się szkoła i wszystko trafił szlag. Ale ciągle pracuję - kompletne archiwum (Neo 1.0) będzie dostępne już niedługo, a kolejne, dużo bardziej rozbudowane wersje już... tuż tuż :) ...

A póki co miłej zabawy i równie ciekawych doświadczeń, jak te przy pisaniu **NeoTrackera**, życzy

epi/Allegresse