# Addendum: AI CV and Job Application Assistant

## Market and domain research (web research digest, 2026-09-23)

### Norwegian tools

- **Karriereveiledning.no** (public career guidance): AI tools for drafting a first application from a CV and job ad, describing skills, and generating interview questions from a job ad. Uses Azure OpenAI hosted in Norway East. https://karriereveiledning.no/kunstig-intelligens-i-veiledning
- **NAV**: human/chat guidance and written tips (tailor to the ad, ~1 page, mirror keywords); no AI generation tool found. https://www.nav.no/soknaden-og-cv
- **FINN.no**: "SmartSøk" and an AI cover-letter text assistant; FINN argues the traditional cover letter is dying ("søknadsbrevet er dødt"). https://www.finn.no/bedriftskunde/aktuelt/jobbindeks/soknadsbrevet-er-dodt
- **Small Norwegian GPT wrappers**: Jobbe.ai, Jobbki.no, Jobbfikser.no, Jobbsoknader.no, SøknadGPT (cvcv.no, pulls ads from Finn), Cover Letter Copilot. Mostly generation only; none found combining generation, review and interview prep. No user-review data found.

### International tools

- Teal (pipeline tracking), Huntr (all-in-one), Rezi (ATS formatting), Kickresume (GPT first drafts), Jobscan (Q&A resume coach, ATS keyword scoring). https://www.jobscan.co/blog/best-ai-resume-builders/
- Kickresume does not list Norwegian as a supported language; no confirmed Norwegian support found for the others.
- Final Round AI: not verified.

### Norwegian application conventions

- Short: roughly 250–400 words, max one page.
- Direct, genuine and engaged tone; not over-formal.
- Structure: an opening naming the position, then experience matched to requirements, then motivation for this specific company, then a short closing.
- Employers value evidence of research into the specific company.
- Open question: Bokmål vs Nynorsk handling.
- Sources: https://www.academicwork.no/artikler/jobbsoker/tips-til-hvordan-du-skriver-et-soknadsbrev, https://www.uia.no/studier/jobb-og-karriere/slik-skriver-du-en-god-jobbsoknad.html

### Known weaknesses of plain ChatGPT

- Generic, overused phrases, missing keywords, too long, and invents skills the user never mentioned. https://www.jobscan.co/blog/using-chatgpt-to-generate-cover-letters/
- Norwegian recruiters spot AI-written applications easily; the value lies in tightening the applicant's own writing rather than full generation. https://hvilkenai.no/beste-ai-til-jobbsoknad/

### Privacy / GDPR

- CVs and applications are personal data. Users have the rights of access, correction, deletion and portability, and can complain to Datatilsynet.
- Retention figures (4 weeks / 1 year) came from Danish sources and are employer-side. Verify with Datatilsynet before citing them as Norwegian law.
- Precedent: Karriereveiledning.no hosts in the Norway region.

### Gap signal

_Updated 2026-09-25: interview prep is now out of scope, so it no longer counts as a differentiator. See "What Makes This Different" in the brief._

Original finding: no tool found combines native Norwegian conventions, a review mode tailored to the job ad, and interview prep. Karriereveiledning.no is the closest, but it is a general guidance site rather than a dedicated app.

## Worked examples from August (grounding cases for co-writing design)

Two separate, unrelated examples.

**Example A: a strength shown in behaviour, not yet used in an application.** When August finishes his own tasks, he looks for more work or asks whether anyone needs help, where others stop for the day. He noticed this himself, and several people have told him so. It is concrete, observable and confirmed by others.

**Why Example A never reached an application:** August was unsure whether it fit, and he cut content to keep letters short enough that recruiters would read them.

**Example B: a real application sentence** (IT-support job, Norwegian):

> "Jeg trives godt med support, og har en driv/lidenskap for å hjelpe andre og levere best mulig sluttprodukt."

It is meant to convey (1) previous IT-support work experience and (2) a passion for helping people. The concrete story behind each point is not yet captured.

**August's follow-up on Example B:** he has always liked helping people. He stays late to finish a job and goes the extra mile to make sure a customer is satisfied. No single defining story sits behind it.

**Why explaining was easier than writing:** in conversation he didn't have to work out how to fit the point smoothly into the letter or how to phrase it. Talking is easy; composing (fit, flow, phrasing) is hard.

**Concrete story surfaced by a situational question** ("when did you last stay later...?"): a user's PC was stuck in a boot loop after a Windows update the team had pushed. August troubleshot and researched most of the day, wanted to try one last fix, and stayed about 1.5 hours after his workday ended until the problem was solved. It shows persistence, ownership, problem-solving and customer focus, all hidden behind "driv/lidenskap for å hjelpe andre".

## Worked example: Example B from sentence to suggestion (moved from the brief's Solution section, 2026-09-25)

This is the worked example the brief refers to.

- *Before:* "Jeg trives godt med support, og har en driv/lidenskap for å hjelpe andre og levere best mulig sluttprodukt."
- *Question:* "When did you last stay longer or do more than you had to for a user?"
- *Answer:* a user's PC was stuck in a boot loop after a Windows update; August troubleshot most of the day and stayed 1.5 hours after his workday ended until it was fixed.
- *Suggested example:* "Da en brukers PC havnet i en oppstartsløkke etter en Windows-oppdatering, feilsøkte jeg store deler av dagen og ble igjen halvannen time etter arbeidstid til problemet var løst."

## Co-writing flow options considered (2026-09-25)

- **A. Gap-finder, then full rewrite:** the app finds ad requirements the draft doesn't show, asks questions, and rewrites the whole draft. Rejected because the app writes too much and the text loses the user's voice.
- **B. Sentence by sentence (chosen):** the app flags a weak sentence, explains why, asks a situational question, and suggests example text. The user accepts it, rewrites it in their own words, or ignores it.
- **C. Coach only, never writes text:** rejected because it brings back the composing problem (fitting points in, flow, phrasing).
