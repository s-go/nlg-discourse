# Fragen

## 2017-05-11

* WebNLG Challenge geeignet für Ansatz von Angeli et al. (2010)?
	* Daten werden immer komplett ausgedrückt
	  * → kein *record choice*, kein *field choice*
	  * unnatürliche Situation
	* teilweise unsinnige Datensets
		"Alan Shepard, who was awarded the Distinguished Service Medal by the US Navy, died in California where the Smilodon fossil was found."
    * Baseline-System: Neural Network

* Angeli et al. (2010), Formel (2)?

* Implementierung?
	* Sprache/Bibliotheken
	* Best practices
* Alignment: veröffentlichten Code verwenden?


## 2017-04-21

* "Automatic Prediction of Discourse Connectives":
	* Eingabe: nur Oberflächenformen, keine semantischen Informationen
* Semantic Correspondence
	* spannend
	* ML-Ansatz herausfordernd
	* Ziel: Template-Kandidaten lernen?
* Daten-Text-Korpora
	* RTR (deuts ch)
		* Hotelbeschreibungen
		* Fußball-Vorberichte
		* Fußball-Spielberichte
		* Rechte/Lizenzen für Forschung?
	* Research (englisch)
		* Weather
		* Robocup
		* NFL
		* Vergleichbarkeit mit Forschung

### Ideen

* Fußball-Tickermeldungen
** verschiedene Ticker
** Frames: Kicktionary

* Lernen
** Prominenz von Ereignissen (über verschiedene Ticker)
** Unterschiede zwischen Tickern

* Problem
** bisher kein Korpus von Tickermeldungen
** [ ] noch zugreifbar?

### To do

* [ ] Daten und Goldkorpus verfügbar?
* [ ] Daten- und Domänenwahl
	* Beispieldaten und -text
* [ ] Sebastian Strober als ML-Mentor?

## 2017-04-04

* formale Anforderungen?
	* Umfang: bei Software-Arbeit 15 Seiten (max. 30)
	* Zeitrahmen
* inhaltliche Anforderungen
	* Ziel?
	* eigenständig arbeiten
	* Software-Arbeit: weniger Text
* Wie theoretisch? Wie praktisch?
* Thema:
	* lieber weit ("Diskursrelationen im Anwendungskontext der automatischen Textgenerierung")?
	* lieber eng (ein Aspekt daraus)?
* regelmäßige Statustreffen (z. B. einmal pro Monat)?
** ab 20.04.

### !
* "Planung und Realisierung von Diskursrelationen"?
* TG2
* Yag (Susan McRoy)
* Theume: Implementierung?
* Sprachspezifika?
* Handygenerator?

* eigentständiges Modul?
	* Input: Diskursmodell für Domäne, Messages

* Diskursmodell aus Korpus lernen (!)
	* Diskursparser (PDTB-/RST-Parser)
	* RST-Parser (Nguyen Sandra)
	* Korpus: rtr?
	* Herausforderung: Clauses auf Abstaktionsebene bringen

* Projekt: Fußballticker
	* Zusammenfassung
	* Scrapen, Parsen, Frames

* Plan C: externes Projekt

* "Predicting Connectives"

