# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G106 – G106-holbein |
| **Product brief** | `_bmad-output/planning-artifacts/briefs/brief-Project-2026-09-23-cv-assistant/brief.md` med `addendum.md` (commit 8ee9c8c) |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Godt utgangspunkt med justeringer.** Gruppen kan gå videre og innarbeide punktene under.

**Det som er bra:**

1. Idéen har en tydelig og gjennomtenkt vri: «the applicant writes, and the app helps». I stedet for å generere søknaden går appen gjennom utkastet setning for setning, flagger det som er generisk, og stiller situasjonsspørsmål («when did you last stay late to fix something?») før den foreslår tekst. Reglene «question before suggestion» og «nothing invented» gjør appen klart forskjellig fra ChatGPT og Jobbki.
2. Omfanget er godt avgrenset for én person: profil og én kjernefunksjon (samskriving og gjennomgang), med CV-generering bare hvis tiden tillater det, og intervjuforberedelse eksplisitt ute. Addendumet viser også at dere har vurdert og forkastet alternative flyter (A og C) med begrunnelse.

**De viktigste endringene:**

1. Gjør suksesskriteriene testbare i appen. Blindtesten med leder og kolleger er et godt mål for nytten, men sensor kan ikke etterprøve den. Legg til kriterier som kan bli tester, for eksempel at appen alltid stiller et spørsmål før den foreslår tekst, at forslaget bare inneholder opplysninger fra profil, utkast og svar, og at ferdig brev er under en bestemt ordgrense.
2. Planlegg språkmodellen og kjørbarheten: hvilken modell, hvor nøkkelen ligger, og en testmodus med ferdige svar, slik at sensor kan prøve hele flyten uten din nøkkel. Dette er særlig viktig fordi hele kjernefunksjonen er KI-basert.
3. Avklar lagring og personvern før arkitekturen. Briefen lister GDPR som åpent spørsmål. Bestem om v1 er en lokal app for én bruker uten innlogging (enklest) eller har kontoer, og hvor profiler og søknader lagres. Vurder også om reelle søknadstekster og personlige eksempler bør ligge i et offentlig repo, eller om de bør erstattes med fiktive testcase.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Middels**

**Sammenlignbart med:** 2) AI CV- og søknadsassistent (middels). V1 er smalere enn forslaget (ingen filopplasting, gap-analyse eller ATS-optimalisering), men kravene til kvalitet i KI-svarene er høyere, fordi appen skal følge faste regler gjennom en flertrinns dialog.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | Middels | Flyten per setning (flagg → forklar → spør → foreslå → bruk/omskriv/ignorer) må holde styr på tilstand, og reglene må håndheves. |
| Datamodell – antall entiteter og relasjoner mellom dem | Middels | Profil (utdanning, ferdigheter, erfaring), stillingsannonse, utkast, setninger, spørsmål, svar og forslag. |
| Brukere, roller og innlogging | Lav–middels | Én brukertype. Uavklart om det trengs innlogging. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | Høy | Vurdering av setninger mot annonsen, målrettede spørsmål og forslag som ikke finner på noe. Briefen peker selv på risikoen for at modellen ikke følger reglene. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | Middels | LLM-API med nøkkel og kostnad. Modell og leverandør er ikke valgt. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | Lav | Ingen. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | Lav | Annonse og utkast limes inn. CV-generering med maler er eventuelt et senere trinn. |
| Sikkerhet og personvern | Middels–høy | Profiler og søknader er personopplysninger, og tekst sendes til en ekstern KI-tjeneste. |

**Hva vanskelighetsgraden betyr for dere:**

- _Middels:_ Et godt balansert valg. Pass på at kjerneflyten blir ferdig og stabil før dere legger til mer. For deg betyr det: profil → annonse → utkast → setning for setning med spørsmål og forslag → ferdig brev. Få reglene til å holde i denne flyten før du ser på CV-generering.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | OK | Én kjernefunksjon pluss profil er realistisk for én person, med tid til iterasjoner på prompts og regler. Kom snart i gang med PRD. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | OK | Flyten i seks steg og reglene gir et svært godt grunnlag for PRD og stories. Det er også bra at briefen er tatt inn via pull request. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | En webapp med skjemaer, lagring og LLM-API er godt dokumentert. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | Risiko | Du kan selv vurdere om forslagene er gode, men å sjekke systematisk at modellen aldri finner på noe er krevende. Lag et fast sett testutkast og sjekk forslagene mot profil og svar. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | Risiko | Reglene er tydelige, men krever tester med mock-svar for flyten og en dokumentert manuell testplan for KI-kvaliteten. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | Stor risiko | Uten testmodus kan ikke sensor prøve kjernefunksjonen. Dette må planlegges i arkitekturen. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | Risiko | Briefen nevner en Norge-hostet modell som sammenligning, men ikke eget valg, kostnad eller testmodus. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart som beskrevet.**

Forutsetningen er at du planlegger testmodus for sensor og avklarer lagring før arkitekturen.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. La v1 være en lokal app for én bruker uten innlogging, med lagring lokalt og en tydelig «slett mine data»-funksjon. Det løser mye av GDPR-spørsmålet og fjerner kompleksitet.
2. Lag en enkel regelkontroll i kode i tillegg til prompten, for eksempel at forslaget ikke kan vises før brukeren har svart på spørsmålet. Da håndheves «question before suggestion» av appen, ikke bare av modellen, og det kan testes automatisk.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Svært tydelig om problemet (å oversette egen erfaring til det arbeidsgiver ser etter) og om den motsatte tilnærmingen. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Konkret, med nyutdannede studenter som målgruppe og en god forklaring av hvorfor eksisterende verktøy ikke løser problemet. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Seks tydelige steg og to grunnregler, beskrevet fra brukerens side. |
| What Makes This Different – er vurderingen ærlig og realistisk? | OK | Ærlig om at ingenting er teknisk vanskelig å kopiere, og at forskjellen ligger i metoden og reglene. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Tydelig primærbruker, og nyttig at dere sier hvem appen ikke er for. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Juster | Kontrollene av ferdig brev (konkret eksempel, maks én side, ingenting oppdiktet) er gode. Legg til kriterier som kan testes i appen, og vurder om blindtesten bør gjøres med fiktive eller anonymiserte søknader. |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | OK | Tydelig kjerne, «if time allows» og «explicitly out». Avklar om innlogging og lagring av flere søknader er med. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | Juster | Briefen mangler en egen visjonsdel. Legg inn et kort avsnitt om hvor appen kan gå etter v1, for eksempel CV-generering og intervjuforberedelse, så det er tydelig at det ikke hører til v1. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | OK | Presis brief, dokumenterte valg i addendumet og bruk av branch og pull request. Fortsett slik. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | OK | Realistisk og tydelig kjerneflyt med nok reell funksjonalitet. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Juster | Reglene egner seg godt som testtilfeller hvis de håndheves i kode og testes med mock-svar. Legg til en manuell testplan for KI-kvaliteten. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Flyten setning for setning gir et tydelig designproblem. Skisser hvordan flaggede setninger, spørsmål og forslag vises side om side med utkastet. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | OK | Ingen teknologivalg i briefen, og det er riktig. Samle LLM-kall og regelkontroll i egne moduler. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Endre | Avhengig av LLM-nøkkel. Planlegg `.env.example`, testmodus og en fiktiv eksempelprofil med annonse og utkast. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Hold nøkler utenfor repoet. Bruk fiktive testdata i repoet, og vurder om personlige eksempler i addendumet bør anonymiseres, siden repoet er offentlig. |

## 3. Neste steg for gruppen

1. Legg til testbare suksesskriterier for reglene og flyten, og en kort visjonsdel.
2. Velg språkmodell, og beskriv testmodus og hvordan sensor kjører appen uten din nøkkel.
3. Bestem lagring og innlogging (gjerne lokal app for én bruker i v1), og gå videre til PRD.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
