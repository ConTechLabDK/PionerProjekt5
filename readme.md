# ConTech Pionerprojekt 5
*Af: Mads Holten Rasmussen, [NIRAS](https://www.niras.dk/)*

Dette repository indeholder en samling [RDF](https://www.w3.org/TR/rdf11-primer/)-filer, som beskriver den test-model, der blev skabt i ConTech Pionerprojekt 5.

Der er i denne sammenhæng også udarbejdet en serie videoer som gennemgår indholdet af dette repository i 5 steps.

## Indhold

### Modeller
Indeholder test-modellen i Revit- og IFC-format. Derudover indeholder mappen filen **Model.pdf** som er en dybdegående beskrivelse af testmodellen, dens opbygning og de forhold, der påvirker væggene, som kan udledes af konteksten.

### RDF
Mappen RDF indeholder den samlede "knowledge base". Heri ligger undermapperne *ABox* og *TBox* som beskriver hhv. assertion-laget og terminologilaget. 

ABox beskriver viden fra vores konkrete testmodel. Eksempelvis:
* "*væg1* er en **Væg**"
* "*væg2* er en **Væg**"
* "*rum5* er et **Rum**"
* "*rum5* har tilstødende bygningsdel *væg1*"

TBox indeholder ontologier der beskriver hvad eksempelvis en **Væg** og et **Rum** er. Eksempelvis at der kan være en relation "tilstødende bygningsdel" imellem dem.

Alle filer er serialiseret i [Turtle](https://www.w3.org/TR/turtle/), men de kan konverteres til eksempelvis [RDF-XML](https://www.w3.org/TR/rdf-syntax-grammar/) eller [JSON-LD](https://www.w3.org/TR/json-ld11/) med et værktøj som [dette](https://www.easyrdf.org/converter).

#### ABox
ABox (datamodellen) er inddelt i følgende filer:
* *bygningstopologi.ttl* beskriver objekter og deres indbyrdes forhold med blandt andet [BOT](https://w3id.org/bot)-ontologien.
* *brandsektioner.ttl* beskriver hvilken brandsektion de enkelte rum tilhører
* *elementegenskaber.ttl* beskriver simple egenskaber som navne og geometrisk afledte attributter.
* *produkter.ttl* indeholder klassifikation af objekter med IFC.
* *rumprogram.ttl* indeholder krav til rum som støj- og fugtforhold.

#### TBox
TBox (ontologier) indeholder en kopi af [BOT](https://w3id.org/bot)-ontologien og en samling af egne termer som blev specifikt defineret til dette projekt. Eksempelvis nogle mere specifikke grænseflader mellem rum og bygningsdele + klassifikation ift. brand.

### RULES
Indeholder to regler (*Saturation1-Fire-resistance.dlog* og *Saturation2-noise-reduction.dlog*) til at udlede brand- og støjkrav til vægoverflader ud fra viden om de tilstødende rum. De er beskrevet i Datalog og kan eksekveres i [RDFox](https://www.oxfordsemantic.tech/product). Derudover indeholder den en række [SHACL](https://www.w3.org/TR/shacl/)-regler til prægranskning af modellen.

### QUERIES
Indeholder en række SPARQL-queries, som forespørger på forskellige forhold i testmodellen.

### SCRIPTS
Scripts som kan køres med [RDFox](https://www.oxfordsemantic.tech/product).

## Prøv det
Diverse test-scripts er udviklet så de kan køres på en [RDFox](https://www.oxfordsemantic.tech/product) triplestore. Det er også muligt at loade ABox og TBox i en anden triplestore som [Fuseki](https://jena.apache.org/documentation/fuseki2/) (open source), [Stardog](https://www.stardog.com/) eller [GraphDB](https://graphdb.ontotext.com/).

1. Installer RDFox
1. Kør det generelle script `C:/RDFox/RDFox sandbox . ./rdfox.script`

### Prægranskning
Udfør prægranskning med denne kommando:
`C:/RDFox/RDFox sandbox . ./SCRIPTS/precheck.script`

### Opkvalificering, test
Disse to scripts dokumenterer at regler for opkvalificering af datamodellen fungerer:
`C:/RDFox/RDFox sandbox . ./SCRIPTS/fire-resistance.script`
`C:/RDFox/RDFox sandbox . ./SCRIPTS/noise-reduction.script`

Byg dokumentation:
`https://shacl-play.sparna.fr/play/doc`

