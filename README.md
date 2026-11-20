# Najem – rozliczenia najmu na telefon

**Wersja 1.3** · prosta aplikacja do pilnowania najmów: comiesięczne należności od najemcy, wpłaty, podatek (ryczałt 8%) i koszty. Działa bez internetu, dane są zapisane **tylko w Twoim telefonie**, chronione PIN-em. Siostrzana aplikacja do „Budżetu domowego”: ta sama technologia i ten sam wygląd.

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

- **Najem** – nazwa, czego dotyczy, najemca, okres od–do (puste „do” = na czas nieokreślony), dzień płatności i pozycje płacone co miesiąc (np. Czynsz najmu, Opłaty). Przy każdej pozycji zaznaczasz, czy liczy się do podatku.
- **Jeden najem = jedna strona** – przełączanie strzałkami ‹ ›, przeciągnięciem palca po karcie podsumowania albo z listy po stuknięciu w nazwę.
- **Należności co miesiąc** – 1. dnia miesiąca pojawiają się same, z terminem płatności i oznaczeniem „po terminie”.
- **💰 Wpłynęło** – okienko z datą wpływu (Dziś / Wczoraj / W terminie / dowolna) i kwotą; pozycja przeskakuje pod dzień wpłaty. Dla minionych miesięcy domyślną datą jest termin płatności. Przyciskiem **✓ 📅** przy opłaconej pozycji zmienisz datę, kwotę (wpłata częściowa) albo cofniesz wpłatę. „Wpłynęło wszystko” opłaca wszystkie pozycje z danego dnia naraz.
- **Starsza umowa** – najem z datą początku w przeszłości („od początku najmu”) i jeden przycisk „Oznacz jako wpłacone w terminie” dla wszystkich zaległych; pojedyncze daty poprawiasz potem przyciskiem ✓ 📅.
- **Lista malejąco po datach** – najnowsze na górze: zaplanowane podatki, bieżące należności, wpłaty, koszty.
- **Podatek** – ryczałt (domyślnie 8%) od wpłat, które wpłynęły w danym miesiącu, płatny w kolejnym miesiącu do 20. Kwota zaokrąglona do pełnych złotych. Datę zapłaty ustawiasz sam (domyślny dzień w Ustawieniach, osobno przy każdym podatku); po 20. aplikacja ostrzega. Zakładka **Podatek** pokazuje wszystkie najmy razem, miesiąc po miesiącu, z podsumowaniem roku i ostrzeżeniem powyżej 100 000 zł przychodu.
- **Koszty i jednorazowe należności** – zielony przycisk **+** (naprawy, ubezpieczenie; dopłata za media, kaucja).
- **Podsumowanie roku** – wpłynęło, podatek, koszty i ile zostaje.
- **Raport** – jeden plik HTML: na komputerze podgląd, na telefonie kopia zapasowa (**Wczytaj z pliku**). Przypomnienie po 7 dniach.
- **Excel** – arkusze: Wpłaty, Podatek, Koszty, Nieopłacone.
- **Motyw** jasny / ciemny (przycisk w prawym górnym rogu), **PIN** z blokadą po minucie w tle.

## Ważne

- Dane są tylko w telefonie. **Odinstalowanie aplikacji lub wyczyszczenie danych Chrome może je usunąć** – wysyłaj raport regularnie.
- Najem i Budżet domowy działają pod tym samym adresem `github.io`, więc dzielą pamięć przeglądarki. Najem używa wyłącznie kluczy zaczynających się od `najem-`, więc dane obu aplikacji się nie mieszają.

## Historia wersji

- **1.3** – przywracanie usuniętych należności (+ → „Przywróć usunięte należności” albo w edycji najmu).
- **1.2** – w menu **+** „Czynsz i opłaty – kwoty co miesiąc” i „Należności za wcześniejsze miesiące”; podpowiedzi na stronie najmu, gdy brakuje kwot lub wcześniejszych miesięcy.
- **1.1** – wybór i zmiana daty wpływu (✓ 📅), dodawanie wcześniejszych należności, „oznacz jako wpłacone w terminie”, zaokrąglanie podatku od 50 gr w górę, motyw tylko przyciskiem na górze.
- **1.0** – pierwsza wersja: najmy, comiesięczne należności, wpłaty, podatek 8%, koszty, raport, Excel, PIN, działanie offline.
