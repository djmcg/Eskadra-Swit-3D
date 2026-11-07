# Eskadra Świt 3D

Pionowa strzelanka 3D w przeglądarce (Three.js / WebGL), pełny ekran, sterowanie myszą, dotykiem lub klawiaturą.
Bronisz wybrzeża w **4 rundach po 10 poziomów**. Każda runda ma inną mapę, innych wrogów i kończy się walką z bossem
o własnej mechanice. Po pokonaniu czwartego bossa kończy się gra („Gratulacje!”).

## Rozgrywka

- **Rundy:** 1 Morze → 2 Pustynia → 3 Zima → 4 Twierdza na lawie. Każda z własnym podłożem, niebem, światłem, scenerią i opadami.
- **Poziomy:** 10 w rundzie (9 zwykłych + walka z bossem). Poziom ma skończoną liczbę wrogów; trudność rośnie z poziomem i rundą.
- **Wrogowie:** myśliwiec, zygzak, bombowiec oraz w każdej rundzie jeden nowy: kamikadze (R1), śmigłowiec bojowy (R2),
  lodowy snajper ze spowalniającym pociskiem (R3). Runda 4 to wyłącznie wieże naziemne (działko, salwa, rakieta naprowadzana, bunkier).
- **Pasek życia:** gracz ma pasek wytrzymałości i kilka żyć. Trafienie zabiera część paska, po jego wyczerpaniu tracisz życie.
  Pasek odnawia bonus „naprawa”, koniec poziomu (+15) i zmiana rundy.
- **Przecieki:** wróg, który przeleci dolną krawędzią, zapełnia licznik przecieków; pełny licznik zabiera część paska (nie dotyczy rundy 4).
- **Bonusy:** broń (4 poziomy), tarcza, naprawa, bomba, zegar, szybki ogień. Są rzadkie (odstęp i limit na poziom zależą od trudności),
  1UP daje tylko pokonany boss.
- **Punkty i rekordy:** osobny rekord dla każdego poziomu trudności.

### Bossowie

| Runda | Boss | Mechanika | Jak pokonać |
|---|---|---|---|
| 1 | **Admirał** | Rdzeń jest opancerzony (20% obrażeń), dopóki działają dwa działa na skrzydłach. | Zniszcz oba działa (pomarańczowe znaczniki), potem rdzeń. |
| 2 | **Gunship Alfa** | Czerwony pas ostrzega przed szarżą przez cały ekran. Po szarży boss jest przegrzany (×2 obrażeń). | Zjedź z pasa w bok, strzelaj w przegrzanego. |
| 3 | **Lodowy Lewiatan** | Pancerz na zmianę zamyka się (nietykalny) i otwiera (cyjan). Zamknięty strzela lodem i pierścieniem pocisków. | Unikaj pocisków, strzelaj tylko przy otwartym pancerzu. |
| 4 | **Cytadela** | Cztery generatory osłaniają rdzeń (im mniej ich, tym większe obrażenia); po zniszczeniu wszystkich odpala obrotowy laser. | Niszcz narożne kopuły, potem rdzeń; uciekaj z toru czerwonej linii. |

Opisy są też w grze: krótki na początku walki, pełny w menu pod przyciskiem **Bossowie**.

### Poziomy trudności

Wybór w menu (klik albo strzałki ↑/↓). Zmieniają m.in. liczbę żyć, obrażenia, HP i szybkostrzelność wrogów, prędkość pocisków,
liczebność fal, częstość bonusów, długość okien na bossach, moment szału bossa i mnożnik punktów.

| | Łatwy | Średni | Trudny |
|---|---|---|---|
| Życia na starcie | 5 | 3 | 2 |
| Obrażenia gracza | ×0,6 | ×1 | ×1,4 |
| HP wrogów / bossów | ×0,8 / ×0,75 | ×1 | ×1,3 / ×1,3 |
| Punkty | ×0,75 | ×1 | ×1,5 |

## Sterowanie

| | |
|---|---|
| Mysz / dotyk | ruch samolotu, ogień automatyczny |
| Klawiatura | strzałki lub WASD; w menu ←/→ wybór samolotu, ↑/↓ poziom trudności |
| Esc / P | pauza i ustawienia |
| M / F | muzyka wł./wył. · pełny ekran |

W menu są **Skróty testowe**: start od dowolnej rundy albo prosto od walki z wybranym bossem (wynik nie trafia do rekordów).

## Uruchomienie

Gra używa modułów ES i plików `.glb`, więc potrzebny jest serwer HTTP (nie działa z `file://`):

```
python3 -m http.server 8000      # potem http://localhost:8000/
```

Three.js (r160), `GLTFLoader` i `BufferGeometryUtils` są w katalogu `vendor/`. Z internetu ładują się tylko czcionki Google Fonts.

## Struktura

```
index.html          cała gra: logika, render, audio (syntezowane w WebAudio), UI
vendor/             three.module.js, GLTFLoader.js, BufferGeometryUtils.js
models/             samoloty gracza i wrogów, wyspy (GLB, low-poly)
models/bosses/      lekkie modele bossów boss1..4_*_lite.glb (płaskie cieniowanie, 4 jednolite materiały)
img/                sprity wyboru samolotu
```

Mapy, nowi wrogowie (śmigłowiec, wieże) i efekty są budowane proceduralnie z brył Three.js. Podłoże każdej rundy to tekstura
generowana w kodzie (kolor + normalne, w rundzie 4 także emisja lawy).

### Modele bossów

W `models/bosses/` leżą lekkie wersje (ok. 1,5–2,7 tys. trójkątów, 25–40 KB). Ciężkie oryginały (`Runda … .glb`, kilkanaście MB)
są w `.gitignore`. Cytadela ma osobny węzeł `Glowa`, który gra obraca w stronę gracza.

## Testy

Gra wystawia pomocnicze funkcje `window.__eskadra` (`symuluj`, `skocz`, `info`, `traf`…), używane w testach logiki
w headless Chromium (Playwright): symulacja walk bez renderowania w czasie rzeczywistym.
