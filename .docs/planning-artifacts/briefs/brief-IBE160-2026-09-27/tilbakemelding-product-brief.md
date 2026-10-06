# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G122 – G122-hjellbakk |
| **Product brief** | `.docs/planning-artifacts/briefs/brief-IBE160-2026-09-27/brief.md` (commit 148280e) |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Bør revideres før dere går videre.** Rett punktene markert «Endre» før dere lager PRD og arkitektur.

**Det som er bra:**

1. Briefen er godt strukturert og følger BMAD-malen, med en tydelig brukerflyt i fem steg (sett opp prosjekt → kjør simulering → møt beslutningspunkter → se konsekvenser → revisjonsspor) og en klar differensiering: «en trener for beslutninger, ikke bare et rapporteringsverktøy».
2. Dere er bevisste på hva «AI» skal bety i v1: en regelbasert motor med kritisk-vei-beregning og Monte Carlo, eventuelt med en språkmodell som formulerer anbefalingene. Det er et realistisk og etterprøvbart valg. Lista over åpne spørsmål viser også god selvinnsikt.

**De viktigste endringene:**

1. Omfanget er for stort for én person i ett semester. MVP-en inneholder prosjektoppsett, kritisk vei, kostprognose, Monte Carlo-risiko, fire beslutningspunkter med KI-forslag, endringsforespørsler med konsekvensberegning, innlogging, audit-logg, Gantt og dashboard. Det tilsvarer hele forslag 3, som allerede er vurdert som vanskelig. Velg en minimal versjon (se forslagene under).
2. Suksesskriteriene må kunne sjekkes i emnet. Pilotkunder blant byggefirmaer, betalingsvilje og «en begrunnelse prosjektlederen stoler nok på» kan ikke måles innen fristen. Briefen er skrevet om til et «reelt produktscenario», men det er appen dere leverer i desember som vurderes. Skriv funksjonelle kriterier, for eksempel «for et testprosjekt med 8 aktiviteter beregner appen kritisk vei og total varighet lik fasit».
3. Beskriv beregningsreglene. Hvordan beregnes tidsplan (avhengigheter og varigheter), kost, og risikoeksponering (sannsynlighet × konsekvens eller Monte Carlo)? Hva utløser hvert beslutningspunkt, og hvordan velges forslagene? Uten dette kan dere ikke kontrollere at koden Claude Code lager, gir riktige svar.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Vanskelig**

**Sammenlignbart med:** 3) KI-styrt simulering av prosjektledelse (byggeprosjekt), som er vanskelig. Briefen følger forslaget nesten punkt for punkt, med samme data inn, data ut og beslutningspunkter, og med innlogging og audit-logg i tillegg.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | Høy | Kritisk vei (CPM), kostprognose, Monte Carlo for risikoeksponering, konsekvensberegning av endringer og regler for fire beslutningspunkter. Alt må stemme og henge sammen. |
| Datamodell – antall entiteter og relasjoner mellom dem | Høy | Prosjekt, WBS-elementer/aktiviteter med avhengigheter, ressurser, kostparametre, risikoer, milepæler, beslutninger, endringsforespørsler og audit-logg. |
| Brukere, roller og innlogging | Middels | Enkel innlogging med én rolle, men audit-logg med bruker og tidsstempel. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | Middels | Regelbasert motor, eventuelt med en språkmodell for å formulere begrunnelser. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | Lav–middels | Ingen integrasjoner i v1. Eventuelt et LLM-API. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | Middels | Endringer skal slå ut «i sanntid» i tidsplan og kost. Det er beregning på forespørsel, ikke ekte sanntid, men Monte Carlo kan ta tid. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | Lav | Ikke nevnt. |
| Sikkerhet og personvern | Middels | Prosjektdata omtales som konfidensielle. I emnet bør dere bruke fiktive prosjekter. |

**Hva vanskelighetsgraden betyr for dere:**

- _Vanskelig:_ Et vanskelig prosjekt gir større mulighet for toppkarakter, men også større risiko. Definer en minimal versjon som sikkert kan bli ferdig, og legg resten i tydelige trinn etterpå. For ByggSim kan minimumsversjonen være: legg inn aktiviteter med varighet, avhengigheter og kost → se Gantt med kritisk vei og total kost → registrer en endringsforespørsel og se konsekvensen før godkjenning. Når dette stemmer med fasit, legger dere til risiko og de andre beslutningspunktene.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | Stor risiko | Hele MVP-en er ikke realistisk for én person med hele BMAD-flyten, testing og README. Repoet har foreløpig bare briefen. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | Risiko | Flyten er tydelig, men beregningsreglene mangler, og mange [ASSUMPTION]-punkter er åpne. Med full MVP blir det svært mange stories. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | Webapp med database, CPM-beregning og et Gantt-bibliotek er godt dokumentert. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | Stor risiko | Kritisk vei kan regnes for hånd på små eksempler, men Monte Carlo og samspillet mellom risiko, tid og kost er vanskelig å kontrollere. Start med deterministiske beregninger som kan sjekkes mot fasit. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | Risiko | CPM og kostberegning egner seg svært godt for tester med fasit, men det krever at reglene er skrevet ut. Suksesskriteriene i dag gir få testtilfeller. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | Risiko | Mulig med lokal database og et ferdig fiktivt eksempelprosjekt. Bruker dere en språkmodell til begrunnelser, trengs en fallback uten nøkkel. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | OK | En regelbasert motor trenger ingen betalte tjenester. Bruk en språkmodell bare som valgfritt tillegg. |

**Konklusjon om gjennomførbarhet:**

- **Lite realistisk uten vesentlige endringer.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. Avgrens v1 til tidsplan og endringshåndtering: prosjektoppsett med aktiviteter og avhengigheter, kritisk vei og Gantt, kostprognose, og beslutningspunktet «endringsgodkjenning» med konsekvensberegning. Risikoregister med enkel risikoeksponering (sannsynlighet × konsekvens) kommer i trinn 2. Monte Carlo, de øvrige beslutningspunktene og språkmodell-begrunnelser kommer i trinn 3.
2. Dropp innlogging i v1, og hold audit-loggen enkel (en liste over beslutninger med tidsstempel). Fjern pilotkunder og betalingsvilje fra suksesskriteriene, og flytt dem til visjonen.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Klart hva ByggSim er og hvilke fire beslutningspunkter den støtter. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Godt beskrevet med regneark og møter som ikke henger sammen med risikoregisteret, og endringer som vurderes isolert. Et konkret eksempel (for eksempel en forsinket leveranse) ville gjort det enda tydeligere. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Fem tydelige steg fra brukerens side. |
| What Makes This Different – er vurderingen ærlig og realistisk? | OK | Ærlig om at dere ikke konkurrerer med MS Project eller Primavera på funksjonsbredde. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Prosjektleder i byggeprosjekt er en tydelig primærbruker. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Endre | Pilotkunder, betalingsvilje og tillit kan ikke måles i emnet. Legg til funksjonelle kriterier med fasit for tidsplan, kost og konsekvens av endringer. |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Endre | Tydelig inn/ut, men «inn» er for stort. Avgrens og del i trinn som foreslått over. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Maskinlæring på historiske data, integrasjoner og porteføljenivå er holdt utenfor v1. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Juster | God struktur og flere commits på briefen. Beregningsreglene må inn, og omfanget må ned, før PRD og stories gir en sporbar plan. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | Endre | For stort for én person. En mindre app som virker godt, gir bedre grunnlag enn en stor app som virker halvveis. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Endre | CPM og kost er ideelle for tester, men kriteriene må skrives som sjekkbare regler med fasit. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Tydelig bruker og flyt. Skisser prosjektoppsettet, Gantt-visningen og visningen der brukeren sammenligner alternativer før godkjenning. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | OK | Ingen teknologivalg i briefen. Hold beregningsmotoren i egne, testbare moduler adskilt fra brukergrensesnittet. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Juster | Planlegg et ferdig fiktivt eksempelprosjekt og eventuell testbruker, og en fallback hvis språkmodell brukes. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Planleggingsdokumentene ligger i den skjulte mappen `.docs/`. Lenk til dem fra README. Planlegg også hvor eksempelprosjekter og testdata skal ligge. |

## 3. Neste steg for gruppen

1. Avgrens MVP-en til tidsplan, kost og endringsgodkjenning, og legg resten i tydelige trinn.
2. Skriv beregningsreglene for kritisk vei, kost og konsekvens av endringer, og lag 2–3 små eksempelprosjekter med fasit.
3. Erstatt pilot- og forretningskriteriene med funksjonelle, testbare kriterier, og gå videre til PRD.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
