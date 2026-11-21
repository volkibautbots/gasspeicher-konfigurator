# Doppelmembrangasspeicher-Konfigurator

Lokale, browserbasierte Einzeldatei zur technischen Vorplanung von Doppelmembrangasspeichern. Keine Anmeldung, kein Netz erforderlich (Three.js r158 ist eingebettet). Optik und 3-D-Bedienung entsprechen dem Behälterverkleidungs-Rechner; dieser Rechner selbst wurde nicht verändert.

**Stand:** 21.11.2026 (Europe/Berlin)

**Datei:** `index.html` – im Browser öffnen (Mac, Windows, iPhone Safari). Für das iPhone ist eine gehostete Bereitstellung später komfortabler, die Datei selbst läuft aber offline.

## Quellen

- Anforderungen und Regeln: Spezifikation aus dem Projektraum sowie `quellen/Projektwissen_Doppelmembrangasspeicher.md`.
- Fachliche Funktionsreferenz: `quellen/Doppelmembran_Konfigurator_erweitert.html` (ältere Stände daneben in `quellen/`).
- **Volumentabelle:** Herstellertabelle, von Volker im Projektraum am 21.11.2026 übermittelt (`volumentabelle-hersteller.csv`). Zusätzlich Original-PDF `quellen/files.pdf` (Baur Folien GmbH, Gasspeichervolumen Doppelmembrangasspeicher, Jan. 2025).
- Stil und Three.js-Einbettung: Behälterverkleidungs-Rechner (Archiv, nur gelesen).

## PDF-Abgleich der Volumentabelle

Werte für ganzzahlige Innendurchmesser 10–40 m und sechs Dachformen (Kegelform 30°, Kugelkappe 1/5 D, 1/4 D, 1/3 D, 2/5 D, 1/2 D) sind 1:1 übernommen. Keine Interpolation. Bei nicht ganzzahligem D oder D außerhalb 10–40 m zeigt das Tool „kein Tabellenwert“.

| Stelle | CSV / Tool | PDF `quellen/files.pdf` | Entscheidung |
| --- | --- | --- | --- |
| D 32 m, KK 1/5, Vol. über BOK | 2280 m³ | 2280 m³ (gleicher Wert) | Unverändert übernommen, markiert als *vermutlich Druckfehler im Herstellerdokument, beim Hersteller prüfen* (Nachbarn 2260 / 2720, evtl. 2480). Nicht korrigiert. |
| D 40 m, KK 1/2, Vol. nutzbar | 13780 m³ | 13780 m³ eindeutig lesbar | Als **normaler Tabellenwert** geführt, Quelle Hersteller-PDF. |

Die Volumentabelle gilt im Menüpunkt „Offene Angaben und Berechnungsgrundlagen“ als **erledigt**, mit dem genannten Prüfhinweis zu D 32 / KK 1/5.

## Umgesetzte Funktionen

- Mehrere Behälter pro Projekt (Fermenter, Nachgärer, Gärrestlager, Sonstiges), Bezeichnung, Innen- oder Außendurchmesser, Wandhöhe, Wandstärke, Beton/Stahl.
- Befestigung: Beton C-Profil (Außenkante, Umfang π(D+2w)) oder Doppelflachprofil (mittig, untere Schiene und Deckprofil je π(D+w)); Stahl nur Deckprofil, optional tatsächlicher Montageumfang.
- Lochabstand 11 cm für Flachprofile (Beton-Doppelflach und Stahl-Deckprofil) → Lochanzahl. C-Profil ohne diese Regel.
- Mauerkronenstreifen 57 cm über π(D+w) nur Beton; Nieten ca. 20 cm plus 5 % Reserve; Klemmleisten ca. 1 m ohne pauschale 5 %; Dichtmasse als offene Position.
- Außenmembran-Ösen ca. 1 m, Abspanngummis (vorläufig ein Gummi je Öse, 5 % Reserve), Gurtwandhalter-Bohrungen ca. 90 cm (vorläufig).
- Mittelstütze optional, Höhe = Wandhöhe + 5 % Innendurchmesser (Beispiel 20 m / 6 m → 7 m).
- 5 % Reserve nur auf Kleinteile (Abspanngummis, Einschlagnieten, Anker, Schrauben).
- Einzel- und Gesamtstückliste mit Menge, Einheit, Rechenweg, Status (festgelegt / vorläufige Annahme / fehlt). Identische Positionen im Projekt zusammengefasst.
- Gasvolumen und Dachhöhe aus der Herstellertabelle; geometrische Kugelkappe/Kegel nur als *geometrischer Richtwert, nicht Herstellerwert*. Freibord geometrisch getrennt, nicht mit dem Tabellen-Nutzvolumen verrechnet.
- Gebläse, Drucksicherungen, Füllstandsmessung, Flansche, Schläuche, Fittings, Gurte/Netz, Membranflächen: Positionen mit Status „Auswahlregel fehlt“ bzw. Menge offen.
- Montage: Gerüst bauseits, Transport/Entladung – vorläufig. Planwerte (2 Monteure, Membranhub ca. 4 h, Mittelstützenhub ca. 2 h) erscheinen nur als Platzhalter in den Eingabefeldern und werden nicht automatisch als Menge übernommen; leere Felder bleiben „Menge offen“ und werden nicht bepreist, eine bewusst eingetragene 0 bleibt 0. Übernachtungen (Monteur-Nächte) im Angebot; Satz nur über die Preisliste, leer = offen.
- Menüpunkt „Offene Angaben und Berechnungsgrundlagen“ je Behälter und Projekt; Bauteilvollständigkeit getrennt von Mengenregel-Vollständigkeit.
- Bemaßte dynamische 2-D-Schnittskizze (SVG) und 3-D-Ansicht (Behälterauswahl, Schnitt/Voll, Mittelstütze mit festem Kronenring ca. 1,5 m Durchmesser, radiale Gurte nach ~90-cm-Teilung und Tragnetz mit eigenen Schaltern; Standardorbit flach und nah in die Schnittöffnung).
- Speichern/Laden (JSON-Datei und localStorage), CSV-Export (UTF-8-BOM, Semikolon), Druckansicht, automatische Neuberechnung. Responsive, offline.

## Angebotserstellung

- **Projektdaten & Konditionen:** Projektname, Kunde, Standort, Angebotsnummer, Datum, Gültigkeit, Bearbeiter, Rabatt (%), Nebenkosten/Frachtpauschale (€), MwSt.-Satz (Standard 19 %, abschaltbar für Netto-Angebot) sowie ein Freitextfeld für Angebotsbedingungen.
- **Automatische Positionsermittlung je Behälter:** Alle Positionen aus Stückliste und Montageansätzen werden automatisch übernommen und in sechs Gewerke gegliedert: **Membranen**, **Profile und Schienen**, **Kleinteile**, **Gebläse und Sicherheitstechnik**, **Montage**, **Übernachtung und Kran**.
- **Keine Standardpreise im Code:** Alle Einzelpreise starten leer. **Preise bleiben lokal in diesem Browser bzw. in Ihrer Preisdatei** (`localStorage` und separate Preislisten-JSON, unabhängig vom Projekt-JSON).
- **Zentrale Preisliste & Überschreibung:** Artikelpreise lassen sich zentral pflegen (sodass identische Artikel in allen Behältern denselben Preis erhalten) und bei Bedarf je Behälterposition über „Indiv.“ gezielt überschreiben.
- **Offene Positionen:** Positionen mit Status `fehlt` / `Auswahlregel fehlt` (z. B. Stoßplatten, Dichtmasse, Montagetage) werden als `Menge offen` bzw. `nach Aufwand / offen` ausgewiesen – niemals als `0 €`. Gleiches gilt für Positionen ohne gepflegten Preis (`auf Anfrage` / `nach Aufwand / offen`). Zwischen- und Projektsummen tragen in diesem Fall den Hinweis *Summe ohne offene Positionen*.
- **Drei Anzeigemodi:**
  1. *Einzelpreise je Position* (mit editierbarem Einzel- und Gesamtpreis),
  2. *Gesamtpreis je Behälter* (Positionen mit Mengen, aber ohne Einzelpreise; Zwischensumme je Behälter),
  3. *Nur Projektsumme* (kompakte Behälterübersicht mit Zwischensummen und Projektsummenblock).
- **Ausgabe:** Druckfertige A4-Angebotsansicht („Angebot drucken / PDF“, funktioniert in allen drei Anzeigemodi mit Hinweis *schematische Mengenermittlung, Montagewerte vorläufig*), Angebots-CSV-Export (UTF-8 mit BOM, Semikolon, Dezimalkomma) sowie vollständige JSON-Sicherung inkl. Abwärtskompatibilität für ältere Einzel- und v1-Projekte.

## Übernahme aus der erweiterten HTML-Version

Übernommen, soweit sie der Spezifikation nicht widersprechen: die sechs Hersteller-Dachformen und die Tabellenstruktur, Geometrieregeln, Montagekennzahlen (Monteure, Kranstunden), Katalog der benannten Bauteile, Projekt speichern/laden, CSV, Prüfung offener Angaben, Beispielbehälter 20 × 6 m und 32 × 8 m (Wandstärke 30 cm illustrativ). Eine Hotelpauschale ist nicht fest hinterlegt, sondern wird nur über die Preisliste gepflegt.

## Widersprüche (Spezifikation gilt)

- **Gebläse:** Die erweiterte Version rechnete eine vorläufige Stückzahl aus max(Produktion, Entnahme) / Leistung. Laut Spezifikation ist das keine bestätigte Auslegung – im Tool keine automatische Menge, Status fehlt.
- **Mauerkronenstreifen:** Statt Pflicht-Handlänge wird der geometrische Ansatz π(D+w) verwendet; Überlappung bleibt offen.
- **11-cm-Löcher:** Auch für das Stahl-Deckprofil, nicht nur für Doppelflachprofil.
- **Dachnamen:** Herstellerbezeichnungen statt nur „Halbkugel/Viertelkugel“ (entsprechen KK 1/2 D bzw. KK 1/4 D).

Die detaillierte Tätigkeitsplanung (einzelne Montagetermine mit Statusmaschine) der erweiterten Version ist zu einer klaren Montage-Stückliste mit denselben Kennzahlen verdichtet.

## Offene Punkte

- Stoßplatten-Anzahl, Segmentlängen, Endabstände, Verpackungseinheiten, Verschnitt.
- Bestätigte Membran-, Gurt- und Netzformeln; Dichtmasse-Verbrauch.
- Herstellerregeln für Gebläse, Drucksicherungen, Sensorik, Flansche/Schläuche/Fittings.
- Verrechnung Freibord ↔ Nutzvolumen; verbindliche Montagezeiten und Krangröße; Verkaufspreise.
- D 32 / KK 1/5 / 2280 m³: Prüfung beim Hersteller.

## Rechenbeispiele (Kontrolle)

**Beton, Doppelflachprofil, D = 20 m, w = 0,30 m, H = 6 m, Mittelstütze ja, Dach KK 1/2 D**

- Dₐ = 20,60 m, Dₘ = 20,30 m, Uₐ = 64,717 m, Uₘ = 63,774 m
- Profile je 63,774 m; Löcher je Schiene ⌈Uₘ / 0,11⌉ = 580
- Streifen 63,774 m (57 cm breit); Nieten ⌈63,774 / 0,20⌉ = 319, inkl. 5 % → 335; Klemmleisten 64 (ohne 5 %)
- Ösen 64, Abspanngummis inkl. 5 % → 68; Gurtbohrungen ⌈Uᵢ / 0,90⌉ = 70
- Mittelstütze 6 + 0,05 × 20 = **7,00 m**
- Tabelle: Dachhöhe 10,0 m, Vol. über BOK 1860 m³, nutzbar 1750 m³
- Geometrischer Richtwert Halbkugel: V = 2/3 π r³ ≈ 2094 m³ (nicht Herstellerwert)

**D = 32 m, w = 0,30 m, H = 8 m, Beton Doppelflach**

- Dₐ = 32,60 m, Dₘ = 32,30 m, Uₘ = 101,473 m
- Mittelstützenhöhe (Formel) 8 + 0,05 × 32 = **9,60 m**
- Tabelle KK 1/5 D: H = 6,40 m, Vol. über BOK **2280 m³** (Prüfhinweis), nutzbar 2040 m³

## Hinweis

Technische Ersteinschätzung, keine verbindliche Planungs-, Hersteller-, Preis- oder Montageauskunft. Die Seite ist unter https://volkibautbots.github.io/gasspeicher-konfigurator/ veröffentlicht; diese Erweiterung (Angebotserstellung und 3-D-Gurte/Netz) ist lokal fertig, aber noch nicht auf GitHub übernommen.
