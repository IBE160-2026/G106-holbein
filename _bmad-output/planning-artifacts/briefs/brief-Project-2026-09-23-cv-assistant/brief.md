---
title: "Product Brief: AI CV and Job Application Assistant"
status: final
created: 2026-09-23
updated: 2026-09-25
---

# Product Brief: AI CV and Job Application Assistant

## Executive Summary

Newly graduated students know what they have done but struggle to turn it into a job application: naming their strengths feels awkward, and linking an experience to what a specific employer wants is hard. AI generators like ChatGPT and Jobbki solve this by writing the letter for the student, which produces generic text that Norwegian recruiters easily spot.

This Norwegian (Bokmål) web app takes the opposite approach: **the applicant writes, and the app helps.** The user saves a profile once, pastes in a job ad and writes a rough draft. The app goes through the draft sentence by sentence, flags what is generic, and asks about specific situations ("when did you last stay late to fix something?") to bring out concrete stories. It then suggests example text built only from the user's own answers, which the user can use, rewrite or ignore. It never invents skills or experiences.

It is an IBE160 course project. Success means a working demo and a blind before/after test in which real readers prefer the revised version of a real application.

## The Problem

Most applicants find the opening of a job application easy: saying who they are and a little about themselves. The hard part comes next: naming their strengths and weaknesses honestly, and explaining how past experience makes them an asset in *this particular* job.

This is hardest for students fresh out of school. Their experience comes from studies, part-time jobs and projects, and it doesn't obviously match what the job ad asks for. They know what they have done, but not how to translate it into what the employer is looking for. The result is either a generic application that could go to any employer, or hours stuck in front of a half-written text.

Today's options don't solve this translation problem. AI tools like ChatGPT, Jobbki and SøknadGPT write the letter *for* the applicant. The result is generic, often too long for Norwegian conventions, and sometimes claims skills the applicant never mentioned. NAV and career services give good general advice but no hands-on help with a specific application.

## The Solution

A Norwegian-language web app that helps applicants turn what they have *done* into what an employer is *looking for*, without writing the application for them.

The key observation: applicants who struggle to describe their strengths in writing can often describe them easily in conversation. Asked "what are you good at?", they give an abstract answer. Asked "when did you last stay late to solve a problem?", they tell a concrete story. The story makes the case on its own, so the applicant never has to praise themselves.

**How it works:**

1. **The user creates a profile once:** a little about themselves, skills, education and experience. It is reused for every application.
2. **The user pastes in a job ad.**
3. **The user writes a rough first draft** for that job. It can be clumsy. The app works from the user's own voice and intent; it does not write from a blank page.
4. **The app goes through the draft sentence by sentence.** Measured against what the ad asks for, it flags sentences that are generic or that claim something without showing it, and explains why each is weak.
5. **For each weak sentence, the app asks a question about a specific situation**, using the profile to aim it ("Your profile says you worked in IT support. Can you tell me about a time you went further than you had to for a user?").
6. **The app suggests example text** based on the user's answer, and fills in fixed parts such as name, contact details and sign-off from the profile. The user decides: use it, rewrite it in their own words, or ignore it. The final wording always belongs to the user.

**Ground rules:**

- **Question before suggestion.** The app always asks the situational question before suggesting text. The profile only helps it choose *what* to ask; it is never used on its own to write suggestions. A profile holds facts ("IT support at X"); the stories that make an application convincing come only from the user's answers.
- **Nothing invented.** The app may only use what is in the profile, the draft and the user's own answers. It never adds skills, experiences or achievements the user did not provide.

The addendum has a worked example in which August's generic IT-support sentence becomes a concrete boot-loop story.

## Who This Serves

**Primary: newly graduated students applying for their first jobs in Norway,** the group described in The Problem. Many also find it uncomfortable to praise themselves in writing.

**Secondary: anyone applying for a job in Norway** who wants help making their own application stronger.

**Not for: people who want an application written for them in seconds.** The whole concept is that the AI and the user work together. Someone unwilling to write a rough draft or answer questions will be better served by a generator.

## What Makes This Different

ChatGPT, Jobbki and similar tools are useful, but they write the application *for* the applicant. This app helps applicants write it *themselves*, step by step, in their own words.

- **The result reads as human because it is.** Norwegian recruiters easily spot AI-generated applications. Here the content comes from the applicant's own experiences, and the final wording is theirs.
- **The method is built in.** A skilled user could prompt ChatGPT to ask questions instead of writing. Most students won't; they type "write me an application". The app gives everyone the method without their having to know it.
- **The rules can't be switched off.** A general chatbot drifts back into writing whole paragraphs and embellishing. The app always asks before it suggests and never adds skills or experiences.
- **Measured against the job ad.** Every flagged sentence is judged against what *this* ad asks for, not against general writing advice.
- **Norwegian conventions are built in.** Short, direct, about one page. The app helps decide what earns a place and what gets cut.
- **The profile is remembered.** The user doesn't retype their background for every application.

**Honest caveat:** none of this is technically hard to copy. The difference lies in the approach and the rules, not in proprietary technology. For a course project that is enough. The claim to prove is that the approach produces better applications than generating them.

## Success Criteria

**The product works if a real application gets better and stays the applicant's own.**

- **Blind before/after test:** August runs his real IT-support application through the app. His boss and a few colleagues read the original and the revised version without knowing which is which, and answer: *"Which one would you call in for an interview, and why?"* Success is a clear preference for the revised version.
- **Checks on the finished letter:**
  - It contains at least one concrete example, not only claims about the applicant.
  - It is one page or less.
  - Nothing in it is invented: every claim traces back to the profile, the draft or the user's answers.
  - The applicant feels it is in their own words and would send it without embarrassment.

**Course deliverables:**

- A working demo of the core flow: profile, job ad, draft, questions and suggestions.
- Documentation of how AI was used in development and how the code was quality-assured.
- A reflection report on the development process, challenges and solutions.

## Scope

**Version 1: core**

- **Profile:** contact details, education, skills and experience, entered once. It aims the app's questions, fills in the fixed parts of the letter and later feeds CV generation.
- **Co-writing and review (one feature):** the user brings a rough draft and a job ad. The app goes through the draft sentence by sentence, asks situational questions and suggests example text the user can adopt, rewrite or ignore.
- **Norwegian (Bokmål) only.**

**Version 1: if time allows**

- **CV generation** from a set of ready-made layouts, built on the profile.

**Explicitly out**

- Interview preparation.
- Generating an application from a blank page. The user must write a first draft.
- Nynorsk and languages other than Norwegian.
- Collecting data the application doesn't need, such as date of birth.

## Open Questions and Risks

- **Privacy (GDPR).** Profiles and applications are personal data. The app must let users see, correct and delete their data, and store no more than it needs. Still to decide: where data is stored, how long it is kept, and what it means that text is sent to an external AI provider for processing. For comparison, Karriereveiledning.no uses a model hosted in Norway.
- **Will the AI follow the ground rules?** "Question before suggestion" and "nothing invented" depend on how the language model is instructed, and models can drift. This needs testing during development and is a natural topic for the reflection report.
