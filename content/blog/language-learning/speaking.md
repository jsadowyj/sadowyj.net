+++
title = 'How I Learn Languages, Part 5: Speaking'
date = 2026-09-26T21:00:00-04:00
draft = false
+++

Everything so far has been reading and listening. Speaking is the most important part of a language, and the hardest.

**I'm not in a rush to speak.** Starting too early locked in bad habits for me. The two that stand out:

- **Leaning on the few words you know.** A small vocabulary means you keep circling the same words, and that's a hard habit to break later.
- **Mistakes become automatic.** If you say the wrong gender or case ending enough times, it turns into a reflex that's hard to unlearn.

This is what worked for me, not a hard rule. I started speaking Romanian at around 3,000 known words in LingQ, and for me that was too early. Next time I'd wait until around 6,000. (LingQ counts every form of a word separately, so that's fewer distinct words than it sounds.)

When I'm ready, I start with anyone in my life who speaks the language. If you can afford it, I highly recommend a tutor on [iTalki](https://www.italki.com) for a few lessons a week. For free practice, I use [OmeTV](#free-practice-with-strangers-ometv).

## Getting the most out of a tutor

A tutor's incentives and a learner's don't line up. Tutors do better when you keep coming back, but the goal is to eventually speak without them, so the learner has to drive the expectations. In my experience, many tutors want to pull up a PowerPoint and walk through grammar rules while charging $20 an hour, which I think is a waste of both time and money. The only way to get better at speaking is to speak, so the goal of every lesson is to maximize the time you spend speaking.

So I set it up like this:

- I do the talking, no matter how bad it is.
- The tutor writes down every mistake they notice as I go instead of interrupting.
- I keep my own list too: every mistake I catch myself making, and every time I get blocked and a word or phrase comes to me in English.
- At natural pauses, I ask them to go over the list with me.
- They only explain *why* something is wrong when I ask.
  - No PowerPoint. I ask them to explain with example sentences instead.

### Choosing what goes into Anki

Those lists, especially the blocks, are how I know a word or phrase is useful enough to cram in Anki. A block means I needed it in a real conversation and didn't have it.

In the beginning, almost every word is worth memorizing in Anki, because you're still in the zone of the 2,000 most frequently used words. That stops being true at an intermediate level. Most of the words you're still missing are rare, and that includes the ones you get blocked on in conversation. The difference is that those are relevant to you. If I got blocked on a word while telling my tutor about my week, it's part of my life, and it'll come up again. A random rare word from a LingQ lesson, like "metallurgy," probably won't. By narrowing my new vocabulary down to the stuff I actually talk about, I keep my Anki workload manageable at an intermediate level.

### Turning mistakes into sentences

For every mistake and block on those lists, I come up with a sentence that uses that word or phrase, about my own life or the conversation I just had. Then I have AI correct them.

Fight the urge to paste the mistakes into AI and have it generate all of the sentences for you. You want sentences that are meaningful to you, because that's really what you're practicing here: how to have meaningful conversations in your target language.

Sometimes I just can't come up with a sentence for a word. When that happens, I write all the other sentences first and leave that one blank. That way the AI has the rest of my sentences as context, so it can write one that still has something to do with me.

For the corrections, I use a custom Claude skill I run as `/romanian-corrections`. I paste my mistakes and blocks under *Greșelile/Blocările* (mistakes/blocks) and my numbered sentences under *Propoziții* (sentences). Here's the full prompt, if you want to adapt it for your own language:

{{< details summary="The /romanian-corrections prompt" >}}
```markdown
---
name: "romanian-corrections"
description: "Correct the user's Romanian practice sentences (Greșelile/Blocările + Propoziții format) and return only the corrected Propoziții list plus brief notes."
---

The user is learning Romanian. They will paste a list of mistakes/blocks under "Greșelile/Blocările:" and numbered practice sentences under "Propoziții:".

The goal is everyday spoken Romanian, not polished written style. Corrections should sound like what a native speaker would actually say in casual conversation, not bookish or formal.
- Keep colloquial forms the user already used when they are correct in speech (e.g. "o să" + subjunctive for the future, "nu-s", "n-am", "ăsta/asta", "din cauza asta"). Don't swap them for formal equivalents like "vor" or "din această cauză".
- Prefer common, conversational words and phrasing over literary or prescriptive choices. Don't flag usages that are standard in everyday speech even if style guides frown on them (e.g. "datorită" for neutral causes).
- Still fix real errors: grammar, agreement, cases, spelling, diacritics, and words that don't fit the meaning.

Do the following:

1. Correct every sentence so it is grammatical and sounds natural in everyday speech, including diacritics (ă, â, î, ș, ț), capitalization, spelling, and word choice.
2. If a sentence is blank or only contains a word or form in parentheses, write a natural, conversational sentence that uses that word or form.
3. If a word or phrase in the mistakes list has no matching sentence, add a sentence for it at the end of the list, continuing the numbering.
4. Output ONLY the "Propoziții:" section, in exactly the same format the user used: the same heading, numbering, and blank lines between sentences. Do not repeat the mistakes list, and do not add bold or other formatting inside the list.
5. After the list, add a short "Notes:" section in English with one line per sentence that changed, explaining the main correction. Skip sentences that were already correct. Keep the notes brief.

If the user says they want no notes, skip step 5.
```
{{< /details >}}

### Turning the sentences into flashcards

Once I have the corrected sentences, I paste them into LingQ as a new lesson. Then I go through the lesson and mark everything I want to memorize:

- **Known words** I want to drill get moved down to **level 4 (Learned)**.
- **New (blue) words** get marked **level 1**.
- **Phrases** I want to memorize get their own phrase LingQs.

![A LingQ lesson made from corrected iTalki sentences, with individual words and multi-word phrases marked as LingQs at different levels](/images/italki_lesson.png)

Then I crank Aminte up to levels 1–4 (New through Learned) and import everything. Since every word and phrase I care about now sits somewhere in that range, Aminte seamlessly creates the flashcards, complete with audio, translations, and [grammar notes]({{< relref "reading-and-anki.md#studying-grammar-with-aminte-notes" >}}).

![Aminte popup in Vocab mode: deck set to Romanian::Lecții pe Italki, 0 sentences of context, word levels from New through Learned, and audio on for both the word and the sentence](/images/aminte_italki_settings.png)
![Aminte advanced settings: First occurrence only off, Suspend lookalikes on, AI notes on at level C1, Automatic Anki tags on, Blank length hints off, Card design sync on](/images/aminte_advanced_settings.png)

Two of the advanced settings matter here:

- **First occurrence only: off.** There's usually more than one sentence with the word or phrase I want to memorize, and I want a card for each one.
- **Blank length hints: off.** With this on, the length of the blank gives away whether the answer is a single word or a phrase. Turning it off makes reviews just a bit harder, which encodes the word/phrase better.

## Free practice with strangers: OmeTV

[OmeTV](https://ome.tv) is a free video chat site that pairs you with random strangers, and it's another great resource. If you're afraid of making mistakes like I am, it's the perfect environment. When I accidentally said "I gave birth in America" instead of "I was born in America" (true story, unfortunately), I just skipped to the next person and will (probably) never have to look them in the eyes again.

The downside is that strangers don't know your life the way an iTalki tutor eventually will. I got really good at introducing myself, my background, and why I'm learning the language, but the conversations rarely went deeper than that.

Still, it's free and super useful. My Romanian speaking practice outside of family was probably about 60% OmeTV and 40% iTalki.

---

[<- Part 4: Listening]({{< relref "lingq-listening.md" >}}) · [Part 6: Intermediate ->]({{< relref "intermediate.md" >}})
