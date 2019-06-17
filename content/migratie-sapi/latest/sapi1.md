---
---

# Constructie query

Om lijsten te kunnen opvragen met de UiTdatabank Search API moet je drie zaken opgeven:

1) De 'collection' waarin moet gezocht worden. Deze zijn gewijzigd tegenover vroeger: voortaan zijn het events, places of organizers. Producties worden niet langer ondersteund.

2) De 'inputparameter(s)': de parameters waarmee je de geselecteerde collectie wil gaan bevragen. Dit kan een vrije zoekterm zijn, een categorisatiefacet, een definitie van een aantal zoekresultaten, etc. Sommige parameters kunnen worden gebruikt als negatie of worden gecombineerd (zie verder).

3) Een API-key. Deze dien je mee te geven in de header. 

Bijvoorbeeld:

- om een full text query binnen de search method in de events collection te lanceren stuur je volgende request:
[https://search.uitdatabank.be/events/?](https://search.uitdatabank.be/events/?)

- om items van het type 'bibliotheek' binnen de xmlview method in de actors collection op te halen stuur je volgende request
[https://search.uitdatabank.be/places/?q=terms.label:"Bibliotheek"](https://search.uitdatabank.be/places/?q=terms.label:"Bibliotheek")

## Input parameters

Onderstaande tabel biedt een mapping van oude inputparameters naar de nieuwe SAPI.
De volledige lijst van mogelijke nieuwe inputparameters is te vinden op https://documentatie.uitdatabank.be/content/search_api_3/start.html

## Events

### ZOEKEN OP WIE / WAT

| Oude naam parameter | Nieuwe naam parameter | Beschrijving | Datatype voor input | Voobeeld |
| q | q | Een vrije zoekterm.  | Text | q=Puppet Shadows, q="Last shadow puppets" |
| agebetween | minAge=..&maxAge=.. | Minimum leeftijd tussen deze twee waarden  | Number Number | minAge=12&maxAge=16 |
| age | minAge | Minimum leeftijd | Number | minAge=18 |
| isfree | maxPrice=0 | Gratis events | Fixed | maxPrice=0 |
| permanent | calendarType:permanent | Permanente events (vb. vaste collecties, monumenten, etc.) | Fixed | calendarType:permanent |

### ZOEKEN OP KRUISVERWIJZINGEN EN KEYWORDS

| Oude naam parameter | Nieuwe naam parameter | Beschrijving |
| k | labels:uitpas | Keywords en tags


### ZOEKEN OP CATEGORIEËN

| Oude naam parameter | Nieuwe naam parameter | Beschrijving | Datatype voor input | Voorbeeld |
| eventtype of thema | terms.label / terms.id | bijv. concert, film, tentoonstelling | terms.label:"Concert" / terms.id:"0.50.4.0.0" |
| locationtype | location.terms.label | bijv. kunstencentrum, bibliotheek,...  | Text | location.terms.label:"Bibliotheek" |

### ZOEKEN OP KALENDERINFORMATIE

| Oude naam parameter | Nieuwe naam parameter | Beschrijving | Datatype voor input | Voorbeeld |
| daterange | Alle evenementen die tussen een bepaalde start- en een bepaalde einddatum plaatsvinden. | Date..Date (yyyy-m-d..yyyy-m-dTH.m) | daterange=2010-04-21..2010-04-28 |
| date | Alle evenementen die plaatsvinden op één of meerdere tijdstippen | Date (yyyy-m-d; yyyy-m-dTH.m) | date=2008-09-19;2008-09-20;2008-09-21 |
| datetype | (d.i. de snelste methode) alle evenementen die tijdens een vastgestelde periode plaatsvinden. | Text (today, tomorrow, thisweek, nextweekend, thismonth, next30days, next3months, next6months, next12months) | datetype=today |

### ZOEKEN OP GEOGRAFISCHE INFORMATIE

| Oude naam parameter | Nieuwe naam parameter | Beschrijving | Datatype voor input | Voorbeeld |
| zip | postalCode | Postcode van de locatie | Number | postalCode=2020 |
| city | address.\*.addressLocality | Stad van de locatie | Text | address.\*.addressLocality:Antwerpen |