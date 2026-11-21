# Najem – rozliczenia najmu na telefon

**Wersja 1.11** · prosta aplikacja do pilnowania najmów: comiesięczne należności od najemcy, wpłaty, podatek (ryczałt 8,5%) i koszty. Działa bez internetu, dane są zapisane **tylko w Twoim telefonie**, chronione PIN-em. Siostrzana aplikacja do „Budżetu domowego”: ta sama technologia i ten sam wygląd.

Pełna instrukcja obsługi jest w aplikacji, w zakładce **❓ Pomoc**.

## Pliki w repozytorium

| Plik | Do czego |
|---|---|
| `index.html` | cała aplikacja |
| `sw.js` | działanie bez internetu i aktualizacje |
| `version.json` | numer najnowszej wersji i lista zmian (sprawdzany w Pomoc → Aktualizacja) |
| `manifest.webmanifest` | nazwa, kolory i ikony aplikacji na telefonie |
| `house-192.png`, `house-512.png`, `house-maskable.png` | ikona – biały domek na zielonym tle |
| `xlsx.full.min.js` | eksport do Excela |
| `README.md` | ten opis |

## Pierwsza instalacja

**Na komputerze (jednorazowo):**
1. Repozytorium musi być **publiczne**: GitHub Pages na darmowym koncie nie działa z prywatnego repozytorium. Publiczny jest tylko kod, Twoje dane nigdy tam nie trafiają.
2. Wgraj wszystkie pliki z tabeli powyżej (`git push` albo **Add file → Upload files**).
3. **Settings → Pages** → Source: **Deploy from a branch**, Branch: **main**, folder **/ (root)** → **Save**.
4. Po 1–2 minutach aplikacja działa pod adresem `https://TWOJ-LOGIN.github.io/najem/`.

**Na telefonie (Android):**
1. Otwórz ten adres w **Chrome** → menu **⋮** → **Zainstaluj aplikację**.
2. Przy pierwszym uruchomieniu ustaw **PIN** (osobny niż w Budżecie) albo wybierz „Bez PIN-u”, potem dodaj pierwszy najem.

## Aktualizacja (dane zostają)

1. Wgraj nowe pliki na GitHuba.
2. Odczekaj 2–3 minuty.
3. W aplikacji: **❓ Pomoc → Aktualizacja → Aktualizuj**. Gdy jest nowa wersja, na zakładce Pomoc widać czerwoną kropkę.

Numer wersji jest w trzech miejscach i musi być wszędzie taki sam: `APP_VERSION` w `index.html`, `version` w `version.json`, `CACHE` w `sw.js`.

## Jak działa

- **Najem** – nazwa, czego dotyczy, najemca, okres od–do (puste „do” = na czas nieokreślony), dzień płatności i pozycje płacone co miesiąc (np. Czynsz najmu, Opłaty). Przy każdej pozycji zaznaczasz, czy liczy się do podatku (domyślnie tylko czynsz).
- **Zmiana czynszu** – w edycji najmu wpisz nową kwotę i wybierz z listy, od którego miesiąca obowiązuje (dowolny – od początku najmu do roku naprzód, także wstecz przy wpisywaniu historii). Wpłaty zapisane ze starą kwotą zmienią się tylko, jeśli to potwierdzisz, a karta najmu pokazuje zapowiedź podwyżki.
- **Notatki** – przy każdej należności i wpłacie (np. „zapłacone w lipcu razem z sierpniem”); widoczne na liście i w Excelu.
- **Jeden najem = jedna strona** – przełączanie strzałkami ‹ ›, przeciągnięciem palca po karcie podsumowania albo z listy po stuknięciu w nazwę.
- **Należności co miesiąc** – 1. dnia miesiąca pojawiają się same, z terminem płatności i oznaczeniem „po terminie”.
- **💰 Wpłynęło** – okienko z datą wpływu (Dziś / Wczoraj / W terminie / dowolna) i kwotą; pozycja przeskakuje pod dzień wpłaty. Dla minionych miesięcy domyślną datą jest termin płatności. Przyciskiem **✓ 📅** przy opłaconej pozycji zmienisz datę, kwotę (wpłata częściowa) albo cofniesz wpłatę. „Wpłynęło wszystko” opłaca wszystkie pozycje z danego dnia naraz.
- **Starsza umowa** – najem z datą początku w przeszłości („od początku najmu”) i jeden przycisk „Oznacz jako wpłacone w terminie” dla wszystkich zaległych; pojedyncze daty poprawiasz potem przyciskiem ✓ 📅.
- **Układ strony najmu** – na górze „Najemca ma zapłacić” (nieopłacone, pogrupowane po miesiącach, od najstarszego) i „Podatek do zapłaty”, niżej „Historia”: wpłaty, zapłacone podatki i koszty od najnowszych, pogrupowane po dniach.
- **Podatek** – ryczałt (domyślnie 8,5%) od wpłat, które wpłynęły w danym miesiącu, płatny w kolejnym miesiącu do 20. Kwota zaokrąglona do pełnych złotych. Datę zapłaty ustawiasz sam: dzień w każdym najmie (puste = jak w Ustawieniach) i osobno przy każdym podatku; po 20. aplikacja ostrzega. Zakładka **Podatek** pokazuje wszystkie najmy razem, miesiąc po miesiącu, z podsumowaniem roku i ostrzeżeniem powyżej 100 000 zł przychodu.
- **Koszty i jednorazowe należności** – zielony przycisk **+** (naprawy, ubezpieczenie; dopłata za media).
- **Kaucja** – kwota w edycji najmu; pojawia się w „Najemca ma zapłacić”, ale nie jest przychodem ani podstawą podatku. Gdy wpłynie, jest w karcie „Kaucja u mnie” z przyciskiem „Rozlicz i zwróć”: potrącenia za szkody, data zwrotu, kwota do zwrotu liczona sama. Zatrzymana część zapisuje się z datą zwrotu (domyślnie bez podatku), szkody ponad kaucję – dopłatą najemcy.
- **Zestawienie roku (wykres)** – zysk, pasek „wpłynęło = zysk + podatek + koszty” z kwotami i procentami oraz słupki miesięcy (stuknij miesiąc – szczegóły); przełączanie lat ‹ ›.
- **Płatność z góry** – w najmie „Kiedy najemca płaci: z góry – w poprzednim miesiącu” i dzień (31 = do końca miesiąca); należność za kolejny miesiąc pojawia się wcześniej, a wpłata liczy się do podatku miesiąca, w którym wpłynęła.
- **Raport** – jeden plik HTML: na komputerze podgląd, na telefonie kopia zapasowa (**Wczytaj z pliku**). Przypomnienie po 7 dniach.
- **Excel** – arkusze: Wpłaty, Podatek, Koszty, Nieopłacone.
- **Motyw** jasny / ciemny (przycisk w prawym górnym rogu), **PIN** z blokadą po minucie w tle.

## Ważne

- Dane są tylko w telefonie. **Odinstalowanie aplikacji lub wyczyszczenie danych Chrome może je usunąć** – wysyłaj raport regularnie.
- Najem i Budżet domowy działają pod tym samym adresem `github.io`, więc dzielą pamięć przeglądarki. Najem używa wyłącznie kluczy zaczynających się od `najem-`, więc dane obu aplikacji się nie mieszają.

## Historia wersji

- **1.11** – zmiana czynszu od dowolnego miesiąca (lista od początku najmu do roku naprzód); możliwość poprawienia wpłat już zapisanych ze starą kwotą.
- **1.10** – własny dzień zapłaty podatku w każdym najmie (Ustawienia = wartość domyślna).
- **1.9** – notatka przy każdej należności i wpłacie; zmiana czynszu od wybranego miesiąca (historia kwot, zapisane wpłaty bez zmian).
- **1.8** – podatek domyślnie tylko od czynszu: opłaty, jednorazowe należności i zatrzymana kaucja domyślnie bez podatku; zmiana „liczyć do podatku” może przeliczyć też zapisane wpłaty; na karcie najmu „z podatkiem / bez podatku” przy każdej pozycji.
- **1.7** – kaucja zwrotna: wpłata bez podatku, karta „Kaucja u mnie”, rozliczenie z potrąceniami za szkody (zatrzymana część = przychód), zwrot w historii, arkusz „Kaucje” w Excelu.
- **1.6** – płatność z góry (za kolejny miesiąc w poprzednim); podatek widoczny przy każdej wpłacie; zestawienie roku jako wykres (zysk, podatek, koszty, słupki miesięcy).
- **1.5** – nowy układ strony najmu: „Najemca ma zapłacić” (po miesiącach, od najstarszego) → „Podatek do zapłaty” → „Historia” (zapłacone, od najnowszych).
- **1.4** – stawka podatku 8,5% (domyślnie; zapisane wcześniej 8% zmienia się samo na 8,5%).
- **1.3** – przywracanie usuniętych należności (+ → „Przywróć usunięte należności” albo w edycji najmu).
- **1.2** – w menu **+** „Czynsz i opłaty – kwoty co miesiąc” i „Należności za wcześniejsze miesiące”; podpowiedzi na stronie najmu, gdy brakuje kwot lub wcześniejszych miesięcy.
- **1.1** – wybór i zmiana daty wpływu (✓ 📅), dodawanie wcześniejszych należności, „oznacz jako wpłacone w terminie”, zaokrąglanie podatku od 50 gr w górę, motyw tylko przyciskiem na górze.
- **1.0** – pierwsza wersja: najmy, comiesięczne należności, wpłaty, podatek 8%, koszty, raport, Excel, PIN, działanie offline.
