Eskadra Świt 3D - pionowa strzelanka 3D (Three.js r160 / WebGL).

4 rundy po 10 poziomów (Morze, Pustynia, Zima, Twierdza na lawie), na końcu każdej boss z własną mechaniką:
Admirał, Gunship Alfa, Lodowy Lewiatan, Cytadela. Pasek życia gracza + życia, trzy poziomy trudności (łatwy/średni/trudny),
skróty testowe w menu. Pełny opis: README.md (w repozytorium na GitHubie).

Uruchomienie: wgraj cały folder (index.html + models/ + img/ + vendor/) na serwer HTTP. Nie działa z file://, lokalnie:
    python3 -m http.server 8000     ->  http://localhost:8000/
Three.js jest w vendor/, z internetu ładują się tylko czcionki Google Fonts.
