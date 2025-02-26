---
type: lecture-cg
title: "Heuristiken"
author: "Carsten Gips (FH Bielefeld)"
weight: 3
readings:
  - key: "Russell2020"
    comment: "Erweiterungen und Heuristiken: Abschnitte 6.2.2, 6.3, 6.5"
  - key: "Ertel2017"
assignments:
  - topic: sheet03
youtube:
  - id: rKqNqYBXuK8
fhmedia:
  - link: "https://www.fh-bielefeld.de/medienportal/m/e5d279fef94d9a37e3b5d15fe9f807e024152e4c65a5a1110bab7871aff45828dba25d086e6a24f6a3a14111304b15f31c9844ff04473788595054d406790a59"
    name: "Direktlink FH-Medienportal: KI Heuristiken"
---


## Wenn die Zeit nicht reicht: Suchtiefe begrenzen

*   Einführung neuer Funktionen:
    1.  `Cutoff-Test` statt `Terminal-Test`

        Beispielsweise bei erreichter Tiefe oder Zeitüberschreitung

    \smallskip

    2.  `Eval` statt `Utility`

        Bewertung der erreichten Position (statt nur Bewertung des Endzustandes)

\bigskip

*   Bedingungen an `Eval`:
    1.  Endknoten in selber Reihenfolge wie bei `Utility`
    2.  Schnell zu berechnen (!)


## Beispiel Schach

*   Mögliche Evaluierungskriterien:
    *   Materialwert: Bauer 1, Läufer/Springer 3, Turm  5, Dame 9
    *   Stellungsbewertung: Sicherheit des Königs, Stellung der Bauern
    *   Daumenregeln: 3 Punkte Vorteil => sicherer Sieg

\smallskip

*   Nutzung gewichteter Features
    $f_i$: \quad $\operatorname{Eval}(s) = w_1f_1(s) + w_2f_2(s) + \ldots$

    *   [Beispiel: ]{.notes}  $w_1 = 9$ und $f_1(s)$ = (# weiße Königinnen) - (# schwarze Königinnen)

\bigskip

*   **Alternativ**: Speicherung von Positionen plus Bewertung in Datenbanken \newline
    => Lookup mit $\operatorname{Eval}(s)$ [(statt Berechnung zur Laufzeit)]{.notes}


## Minimax mit mehreren Spielern

::: slides
\bigskip
![](images/minimax3.png){width="90%"}
:::

::: notes
![](images/minimax3.png){width="50%"}
:::

[Tafelbeispiel]{.bsp}

::: notes
Hier maximiert jeder Spieler sein eigenes Ergebnis.  Im Grunde müsste diese
Variante dann besser "Maximax" heissen ...

Wenn es an einer Stelle im Suchbaum mehrere gleich gute (beste) Züge geben
sollte, kann der Spieler Allianzen bilden: Er könnte dann einen Zug auswählen,
der für einen der Mitspieler günstiger ist.
:::


## Zufallsspiele

::: center
![](https://live.staticflickr.com/3670/11267311625_e4758ff425_o_d.jpg){width="60%"}

[Quelle: ["position-backgammon-decembre"](https://www.flickr.com/photos/83436399@N04/11267311625) by [serialgamer_fr](https://www.flickr.com/photos/83436399@N04), licensed under [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/?ref=ccsearch&atype=rich)]{.origin}
:::

Backgammon: Was ist in dieser Situation der optimale Zug?


## Minimax mit Zufallsspielen: ZUFALLS-Knoten

::: slides
\bigskip
![](images/expectimax.png){width="90%"}
:::

::: notes
![](images/expectimax.png){width="50%"}
:::

::: notes
Zusätzlich zu den MIN- und MAX-Knoten führt man noch Zufalls-Knoten ein, um
das Würfelergebnis repräsentieren zu können. Je möglichem Würfelergebnis $i$
gibt es einen Ausgang, an dem die Wahrscheinlichkeit $P(i)$ dieses Ausgangs
annotiert wird.
:::

=> Für Zufallsknoten **erwarteten** Minimax-Wert (*Expectimax*) nutzen

[Tafelbeispiel]{.bsp}


## Minimax mit Zufall: Expectimax

Expectimax-Wert für Zufallsknoten $C$:

$$
    \operatorname{Expectimax}(C) = \sum_i P(i) \operatorname{Expectimax}(s_i)
$$

\bigskip

*   $i$ mögliches Würfelergebnis
*   $P(i)$ Wahrscheinlichkeit für Würfelergebnis
*   $s_i$ Nachfolgezustand von $C$ gegeben Würfelergebnis $i$

::: notes
Für die normalen Min- und Max-Knoten liefert `Expectimax()` die üblichen
Aufrufe von `Min-Value()` bwz. `Max-Value()`.

Auf [wikipedia.org/wiki/Expectiminimax](https://en.wikipedia.org/wiki/Expectiminimax)
finden Sie eine Variante mit einem zusätzlichen Tiefenparameter, um bei einer bestimmten
Suchtiefe abbrechen zu können. Dies ist bereits eine erweiterte Version, wo man beim
Abbruch durch das Erreichen der Suchtiefe statt `Utility()` eine `Eval()`-Funktion
braucht. Zusätzlich kombiniert der dort gezeigte Algorithmus die Funktionen
`Expectimax()`, `Min-Value()` und `Max-Value()` in eine einzige Funktion.

Eine ähnliche geschlossene Darstellung finden Sie im [@Russell2020, S. 212].

**Hinweis**: Üblicherweise sind die Nachfolger der Zufallsknoten gleich wahrscheinlich.
Dann kann man einfach mit dem Mittelwert der Bewertung der Nachfolger arbeiten.
:::


## Wrap-Up

*   Minimax:
    *   Kriterien zur Begrenzung der Suchtiefe, Bewertung `Eval` statt `Utility`
    *   Erweiterung auf $>2$ Spieler
    *   Erweiterung auf Spiele mit Zufall: *Expectimax*







<!-- DO NOT REMOVE - THIS IS A LAST SLIDE TO INDICATE THE LICENSE AND POSSIBLE EXCEPTIONS (IMAGES, ...). -->
::: slides
## LICENSE
![](https://licensebuttons.net/l/by-sa/4.0/88x31.png)

Unless otherwise noted, this work is licensed under CC BY-SA 4.0.

### Exceptions
*   Image ["position-backgammon-decembre"](https://www.flickr.com/photos/83436399@N04/11267311625) by [serialgamer_fr](https://www.flickr.com/photos/83436399@N04), licensed under [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/?ref=ccsearch&atype=rich)
:::
