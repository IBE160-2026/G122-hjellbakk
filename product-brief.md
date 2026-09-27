---
title: "Product Brief: ByggSim — AI-styrt simulering av prosjektledelse"
status: draft
created: 2026-09-27
updated: 2026-09-27
---

# Product Brief: ByggSim — AI-styrt simulering av prosjektledelse

## Executive Summary

ByggSim er en nettbasert simulator for prosjektledelse i byggeprosjekter, der en AI-motor fungerer som beslutningsstøtte gjennom hele prosjektets livsløp. Prosjektledere legger inn omfang (WBS), ressurskapasitet, kost- og tempoparametre, kjente risikoer og milepæler. Simulatoren genererer tidsplaner (Gantt), kostprognoser og risikoeksponering, og kjører scenarier ("hva skjer hvis..."). Ved fire kritiske beslutningspunkter — planstrategi, risikorespons, ressursallokering og endringsgodkjenning — foreslår den konkrete tiltak.

Byggeprosjekter er notorisk vanskelige å planlegge presist — ressurser flyttes, risikoer materialiserer seg, og endringsforespørsler kommer inn midt i gjennomføringen. I dag håndteres dette manuelt i regneark og møter, med beslutninger som ofte er reaktive og dårlig dokumentert i etterkant. ByggSim gir prosjektledere et verktøy for å teste beslutninger mot en modell før de tas i virkeligheten, og etterlater et revisjonsspor (audit-logg) av hvorfor hver beslutning ble tatt.

## The Problem

Prosjektledere i byggebransjen balanserer kontinuerlig tid, kost og risiko under usikkerhet. Dagens praksis:

- Tidsplaner og kostprognoser vedlikeholdes ofte i regneark eller separate verktøy (MS Project, Excel) som ikke snakker sammen med risikoregisteret.
- Risikorespons og ressursallokering besluttes ofte ad hoc, i møter, uten systematisk scenariotesting av alternativer.
- Endringsforespørsler (change requests) evalueres isolert, uten et helhetlig bilde av hvordan de slår ut på tidsplan, kost og risikoeksponering samtidig.
- Beslutningsgrunnlaget dokumenteres sjelden godt nok til at det kan revideres eller læres av i etterkant.

Konsekvensen er at beslutninger tas med ufullstendig informasjon, og at kostbare feilvurderinger (forsinkelser, overskridelser) ofte oppdages for sent til å rettes opp uten store kostnader.

`[ASSUMPTION]` Målgruppen har grunnleggende digital kompetanse og er kjent med begreper som WBS, Gantt og risikoregister fra eksisterende praksis (f.eks. PMI/IPMA-rammeverk), så produktet trenger ikke å lære bort prosjektledelse fra bunnen.

## The Solution

ByggSim er en webapplikasjon der brukeren:

1. **Setter opp prosjektet** — legger inn WBS/omfang, ressurskapasitet, kost- og tempoparametre, og et innledende risikoregister.
2. **Kjører simuleringen** — systemet beregner tidsplan (Gantt), kostprognose og aggregert risikoeksponering basert på inputen.
3. **Møter beslutningspunkter** underveis — planstrategi, risikorespons, ressursallokering, endringsgodkjenning — der AI-motoren presenterer scenarier og anbefalte tiltak med begrunnelse.
4. **Ser konsekvenser** — hver beslutning oppdaterer tidsplan/kost/risiko i sanntid, slik at brukeren kan sammenligne alternativer før de committer.
5. **Får et revisjonsspor** — hver beslutning, endring og AI-anbefaling logges med versjon og tidsstempel (audit-logg).

`[ASSUMPTION]` AI-komponenten i første versjon er en regelbasert/heuristisk motor kombinert med enkle simuleringsmodeller (Monte Carlo for risikoeksponering, kritisk-vei-beregning for tidsplan), eventuelt supplert med en LLM for å formulere anbefalinger i naturlig språk. Fullverdig maskinlæring på historiske prosjektdata er utenfor MVP-scope.

## What Makes This Different

- **Beslutningspunkt-sentrert, ikke skjema-sentrert**: I stedet for bare å vise dashboards, tvinger simulatoren brukeren gjennom eksplisitte beslutningspunkter med anbefalte alternativer og synlige konsekvenser — det er en trener for beslutninger, ikke bare et rapporteringsverktøy.
- **Integrert tid-kost-risiko-modell**: Endringer i én dimensjon (f.eks. en risikohendelse) slår automatisk ut i tidsplan og kostprognose, i stedet for at brukeren må oppdatere tre separate verktøy manuelt.
- **Innebygd audit-logg**: Beslutningshistorikk er en kjernefunksjon, ikke et tillegg — viktig gitt at prosjektdata regnes som konfidensielle.

`[ASSUMPTION]` Vi konkurrerer ikke med etablerte verktøy som MS Project eller Primavera på funksjonsbredde — differensieringen er scenariosimulering og AI-anbefalinger på et avgrenset sett beslutningspunkter, ikke generell prosjektstyring.

## Who This Serves

**Primær bruker:** Prosjektleder i et byggeprosjekt som trenger å teste beslutninger (ressursallokering, risikorespons, endringshåndtering) mot en modell før de tas i virkeligheten, og som trenger et dokumentert grunnlag for beslutningene.

`[ASSUMPTION]` **Sekundær bruker:** Prosjekteier/styringsgruppe som konsumerer output (Gantt, kostprognose, risikoeksponering) i beslutningsmøter, uten selv å legge inn data.

Suksess for brukeren ser slik ut: raskere og bedre begrunnede beslutninger ved kritiske punkter, og et tydelig spor av hvorfor en beslutning ble tatt hvis den senere må forsvares eller revideres.

## Success Criteria

`[ASSUMPTION]` Gitt at dette er et kursprosjekt, foreslås suksesskriterier tilpasset en leveranse/demo snarere enn produksjon:

- En bruker kan sette opp et prosjekt (WBS, ressurser, risikoer, milepæler) og få generert en tidsplan og kostprognose uten manuell etterbehandling.
- Systemet presenterer minst de fire definerte beslutningspunktene (planstrategi, risikorespons, ressursallokering, endringsgodkjenning) med minst ett AI-generert forslag hver, med synlig begrunnelse.
- En endring i én input (f.eks. en risikohendelse inntreffer) forplanter seg synlig til tidsplan og kostprognose.
- Alle beslutninger og endringer er sporbare i en audit-logg med tidsstempel og bruker.
- Løsningen kan demonstreres end-to-end på et realistisk (om enn forenklet) eksempelprosjekt.

## Scope

**Inn i første versjon (MVP):**
- Prosjektoppsett: WBS/omfang, ressurskapasitet, kost/tempo-parametre, risikoregister, milepæler.
- Simuleringsmotor: kritisk-vei tidsplanberegning, kostprognose, aggregert risikoeksponering.
- De fire beslutningspunktene med AI-genererte forslag og begrunnelse.
- Endringsforespørsler: registrering og konsekvensberegning (tid/kost/risiko) før godkjenning.
- Innlogging (enkel autentisering) og audit-logg for beslutninger.
- Visualisering: Gantt-diagram, kost- og risikodashboard.

**Eksplisitt utenfor scope (v1):**
- Multi-tenant/organisasjonsadministrasjon utover enkel brukerinnlogging.
- Maskinlæring trent på historiske/eksterne prosjektdata.
- Integrasjon med eksterne PM-verktøy (MS Project, ERP, regnskap).
- Mobilapp — kun web.
- Betaling/kjøp — ikke relevant, bekreftet i oppgaven.

`[ASSUMPTION]` Skop er trukket stramt for å være realistisk innenfor kursets tidsramme; audit-logg og innlogging er beholdt fordi oppgaveteksten eksplisitt krever det, selv om det øker kompleksiteten.

## Vision

`[ASSUMPTION]` Utover kursleveransen: ByggSim kunne vokse til et fullverdig beslutningsstøtteverktøy for byggebransjen, der AI-motoren læres opp på anonymiserte historiske prosjektdata for å gi stadig bedre kalibrerte anbefalinger, med integrasjon mot eksisterende PM- og ERP-systemer, og støtte for porteføljenivå (flere prosjekter samtidig) for større entreprenører.

---

## Open Questions

- Hvor mye av "AI"-kravet forventes å være ekte modellbasert intelligens (simulering/optimalisering) versus i hvilken grad en LLM skal generere anbefalingstekst? Kurset kan ha spesifikke forventninger her.
- Er det et krav om flerbrukersamarbeid (flere prosjektledere på samme prosjekt) eller er én bruker per prosjekt tilstrekkelig for MVP?
- Finnes det en vurderingsrubrikk fra kurset som bør sjekkes mot scope og success criteria over, gitt at brief-en er skrevet uten tilgang til den?
