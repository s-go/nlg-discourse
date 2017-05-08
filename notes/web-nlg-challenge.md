# The WebNLG Challenge: Generating Text from RDF Data

## Input Scenarios

* **Data:** set of triples extracted from DBPedia (RDF)
	* each triple set contains 1 to 7 triples
	* modified to ensure consistency and homogeneity throughout the data
	* To train models, the modified triples should be used.
* **Text:** a verbalisation of these triples, collected using crowdsourcing
	* each scenario features 1 to 3 verbalizations

**Example:**

```xml
    <entry category="Astronaut" eid="Id1" size="3">
      <originaltripleset>
        <otriple>Alan_Bean | mission | Apollo_12</otriple>
        <otriple>Apollo_12 | operator | NASA</otriple>
        <otriple>Apollo_12 | crew1Up | David_Scott</otriple>
      </originaltripleset>
      <modifiedtripleset>
        <mtriple>Alan_Bean | was a crew member of | Apollo_12</mtriple>
        <mtriple>Apollo_12 | operator | NASA</mtriple>
        <mtriple>Apollo_12 | commander | David_Scott</mtriple>
      </modifiedtripleset>
      <lex comment="good" lid="Id1">Alan Bean was under commander David Scott on Nasa's Apollo 12 mission.</lex>
      <lex comment="good" lid="Id2">Alan Bean was a member of the NASA operated Apollo 12 crew commanded by David Scott.</lex>
      <lex comment="good" lid="Id3">David Scott was the commander of the NASA operated Apollo 12 flight mission on which the crew included Alan Bean.</lex>
    </entry>
```

### Domains

* Airport
	> Abilene Regional Airport serves the city of Abilene which is part of Taylor County,Texas, in the United States.
* Astronaut
	> Alan Bean was under commander David Scott on Nasa's Apollo 12 mission.
* Building
	> South Africa is the location of 11 Diagonal Street. The capital is Cape Town and the leader is Cyril Ramaphosa.
* Comics character
	> The comic character Auron was created by Walt Simonson and the American, Karl Kesel.
* Food
	> From Spain, Ajoblanco (alternatively known as Ajo blanco) has bread as an ingredient.
* Monument
	> Adams County, Pennsylvania is the location of the 11th Mississippi Infantry monument. Franklin County Pennsylvania is to the west and Frederick County to the south west.
* Sports team
	> Massimo Drago played for the club SSD Potenza Calcio and his own club was Calcio Catania. He is currently managing AC Cesena.
* University
	> The Accademia di Architettura di Mendrisio is in Switzerland. Its dean is Mario Botta and it has 600 students.
* Written work
	> Eric Flint is the author of 1634: The Ram Rebellion which has 512 pages and is available as an E-Book.

### Corpus Metrics

#### Dev Corpus

| data set | entries | lexicalizations |
|----------|--------:|----------------:|
| 1triples |     226 |             532 |
| 2triples |     152 |             415 |
| 3triples |     171 |             452 |
| 4triples |     162 |             440 |
| 5triples |     116 |             307 |
| 6triples |      23 |              64 |
| 7triples |      22 |              58 |
| **total**|     872 |            2268 |

#### Training Corpus

**total:** 6940 scenarios, 18102 lexicalizations

## Baseline System

* http://talc1.loria.fr/webnlg/stories/baseline.html
* A preprocessing script extracts tripleset-lexicalisation pairs, linearise triples, performs tokenisation and delexicalisation using the exact match, and writes source and target files.

source files *.triple:
```
COUNTRY leaderName LEADERNAME
FOOD region COUNTRY
FOOD ingredient INGREDIENT
FOOD country COUNTRY
```

target files *.lex:
```
FOOD is a food containing INGREDIENT ; it is found in COUNTRY where LEADERNAME is the leader .
```
* A simple sequence-to-sequence model with the attention mechanism was trained using the OpenNMT toolkit

## Evaluation

Evaluation of the generated texts will be done both with automatic evaluation metrics (BLEU, TER or/and METEOR) and using human judgements obtained through crowdsourcing. The human evaluation will seek to assess such criteria as fluency, grammaticality and appropriateness (does the text correctly verbalise the input data?).

## Timeline

* 14 April 2017: Release of Training and Development Data
* 30 April 2017: Release of Baseline System
* 18 August 2017: Release of Test Data
* 25 August 2017: Entry submission deadline
* 5 September 2017: Results of automatic evaluation and system presentations (at INLG 2017)
* 30 September 2017 : Results of human evaluation

## Our Approach

* Apply an approach similar to **Angeli et al. (2010)** to the challenge.

### Adaptions

* **Simplification:** Since, in general, all the information in the data is expressed in the lexicalizations, we can omit the record choice and field choice models.
* No record types, no field types – instead: RDF triples with subject, predicate and object, e.g.
	* ``Alan_Bean | was a crew member of | Apollo_12``
	* ``Alan_Shepard | deathDate | "1998-07-21"``
	* ``Buzz_Aldrin | alternativeNames | "Edwin E. Aldrin, Jr."``
	* ``Buzz_Aldrin | timeInSpace | "52.0"(minutes)``
	* ``California | fossil | Smilodon``
	* ``Elliot_See | status | "Deceased"``

* Predicates: similar to categorial fields
	* ``birthDate`` correlates with "born", "born on", "on"
* Often: coreference within triple set
	```xml
      <modifiedtripleset>
        <mtriple>California | fossil | Smilodon</mtriple>
        <mtriple>Alan_Shepard | deathPlace | California</mtriple>
        <mtriple>Alan_Shepard | awards | Distinguished_Service_Medal_(United_States_Navy)</mtriple>
      </modifiedtripleset>
      <lex comment="good" lid="Id3">Alan Shepard, who was awarded the Distinguished Service Medal by the US Navy, died in California where the Smilodon fossil was found.</lex>
```

### Lexicalization models

* **Named entities:** replace underscore by spaces
	* ``A.C._Cesena``: "A.C. Cesena"
	* ``Estadio_Jorge_Calero_Suárez``: "Estadio Jorge Calero Suárez"
	* sometimes substring: ``Stuart_Parker_(footballer)``: "Stuart Parker"
* **Dates:** all kinds of formats in lexicalizations
	* ``"1998-07-21"``: "July 21 1998", "21st of July, 1998", "23rd July 1927", "1927-07-23", "October 17th, 1933", "17 October 1933"
	* for generation: rather stick to one format consistently
* **Value-unit pairs:**
	* ``"52.0"(minutes)``: 52 minutes