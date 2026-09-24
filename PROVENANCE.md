# PROVENANCE — how this rendering came to be

*Sorani Kurdish (کوردیی سۆرانی), chair 96. Lit and burned 2026-09-24.
Floor 23,213 verses, 305,507 token rows.*

This is the record of how the text in this repository was produced and
what went wrong with it. A machine-assisted rendering has no standing
unless you can see how it was made, so this file says both.

---

## The approach

Every verse is rendered from the Hebrew of that verse — OSHB / WLC 4.20 —
under a written discipline: `docs/methodology/translation-discipline/ckb.md`
in the Selah repository (commit `25709a6a`), itself written in Sorani,
built on the Kurmanji chair's Name decisions, the Uyghur chair's
Perso-Arabic right-to-left mechanics, and the Bulgarian chair's rails.
Seven rules govern it: the Hebrew token is the unit; the Name stays the
Name; both truths of Deut 6:4; no foreknowledge (Gen 22:1 does not know
Gen 22:13); numbers and marks stay put; the translator has no word of his
own; a hard verse goes in bare.

**The `⟨ ⟩` brackets do two different jobs.** `⟨את⟩` is the Hebrew
direct-object marker, which Sorani has no word for; it is left standing
so the reader sees it. `⟨وشە⟩` is a word Hebrew did not write but Sorani
grammar requires — visibly marked, so you can always tell what the Hebrew
said from what the grammar needed.

The rendering was produced with `glm-5.3` at tier `glm-5.2`, every verse,
through the relay (`batch/relay-move-on! [:ckb]`), engine-side.

## The fight on this chair is the script

Sorani, Persian and Arabic share an alphabet. The model has seen far more
Persian and Arabic than Sorani, so when it tires it slides toward them —
and the result stays readable, which is what makes it dangerous. The
thermometer is therefore built on letters, not words:

| probe | what it catches |
|---|---|
| ث ذ ص ض ط ظ ة | Arabic spellings of loans Sorani respells (صبر → سەبر) |
| ك U+0643 · ي U+064A | the Arabic twins of Sorani ک U+06A9 · ی U+06CC |
| final ه | Persian, where Sorani writes ە U+06D5 (که → کە) |
| Persian whole words | است, این, از, در, بود, گفت — whitelist first |
| one Latin letter | Kurmanji, this chair's sibling in the other script |
| ڕ · ڵ as a rate | their loss is the slide made visible |

Every class is read on **both surfaces**, the flow and the token row. The
row carried more damage than the flow in every round.

## The Name

| Hebrew | here | rejected |
|---|---|---|
| יהוה | **یاهوە** | خودا · خواوەند · پەروەردگار · یەهۆوا · یەهۆڤا · ئەڵڵا · ڕەب |
| אלהים | **ئێلۆهیم** | خودا in the Name's place |
| אל · אל שדי | **ئێل** · **ئێل شادای** | خودای توانادار alone |
| אדני | **ئادۆنای** | خواوەند · پەروەردگار |
| יה · צבאות | **یاه** · **سەڤائۆت** | ی سوپاکان |
| אהיה אשר אהיה | **ئێهیێ ئەشێر ئێهیێ** | من ئەوم کە هەم |

خودا and خوداکان remain lawful over the nations' gods and over a common
noun; the census applies that distinction by the token's Hebrew surface,
never by the Sorani spelling.

## The burn and the gate

A first-hour gate (`dev/scripts/ckb_gate.clj`) read Genesis 1:1 by eye
against the rails, then ran on every batch: the Name, the את family, the
Arabic letters, the final-ه set, Latin inside Sorani words. It caught the
Name's spelling drift at 867 seats and the ك/ي class at 26 flows, both of
which became repair passes.

The relay rendered 23,197 of 23,213; sixteen tail batches timed out and
were gleaned with `translate-corpus-batched!`. The corpus was committed
to git **before any repair pass touched it** (`e4169c99`), so every cure
below is a diff you can read.

## Finding: a spelling repair had to be taught to read the token

The first census found 193 seats drifted off یاهوە. The obvious cure — a
spelling substitution — was run as a dry run first, and the dry run
caught what it would have destroyed: **Jehu** (יהוא → یاهوو),
**Jehoiakim** (یاهوویاکیم), and every *-yahu* name (بێرێخیاهوو). The
drifted Name and a legitimate human name share a spelling.

The cure was rewritten to key on the Hebrew token and nothing else. It
then cured 22 surfaces on 20 seats and left the names alone. Every later
round re-ran it, because a re-press re-renders the verse and can bring
the class back; the pass is idempotent by design.

## Finding: the chair had rewritten a quarter of the Hebrew surfaces

The gate saw it early — around 924 rows, roughly a quarter of the verses
sampled, carried a `surface` the chair had written rather than the
record's. The census, however, reported only **10** corrupt surfaces,
because the probe asked whether the surface contained non-Hebrew
characters, and the damage was subtler: **one Arabic letter fused into an
otherwise Hebrew string** — `وאת` for `ואת`, Arabic waw standing in for
Hebrew vav. Perso-Arabic and Hebrew run in the same direction, and the
letters are cognate, so the substitution is invisible to a character-class
probe and to the eye.

It surfaced sideways. `marker_adjudicate`, run to explain the marker gap,
reported 42 **row** surfaces with an Arabic letter inside the Hebrew. That
report, not the census, is what opened the class. `lang-surface-repair`
(`:bare` convention) then restored **8,364 Hebrew token surfaces across
5,335 verses** from the text — verified surfaces-only, then re-indented
with the fleet's JSON writer.

**The lesson for the next chair: when the chair's script is cognate with
Hebrew, the surface probe must compare against the record, not test the
characters.**

## The cure, in order

| pass | what |
|---|---|
| gleaning | 16 holes the relay's tail left |
| repairs 1 | the Name's drift (22 surfaces, 20 seats, token-guided) · Arabic ك→ک ي→ی (548 surfaces) · 204 files |
| re-press 1 | **1,468** convicted seats (press 1,391 · ladder 77 · 0 failed) |
| repairs 2 | the ك/ي the re-press brought back (15 files) |
| re-press 2 | **348** seats (press 336 · ladder 12) |
| repairs 3 | 7 files |
| re-press 3 | **143** seats (press 140 · ladder 3) |
| repairs 4 | 1 file |
| re-press 4 | **67** seats (press 61 · ladder 6) |
| repairs 5 | 3 files |
| re-press 5 | **45** seats, all pressed |
| repairs 6 | 2 files |
| surface restoration | **8,364** Hebrew surfaces in 5,335 verses |

Across the rounds the structural classes went to zero — empty token rows,
count mismatches, corrupt surfaces, Latin letters, Hebrew leaking outside
the markers, fabricated markers — and the marker gap fell
**1,202 → 310 → 129 → 33 → 10**.

## Open — declared, not repaired

- **Five stubborn seats** that survived all five re-press rounds:
  exodus/2/15 (`میدjan`) · nehemiah/5/13 (`لێdam`) · hosea/3/5 (an IPA ɪ)
  · exodus/8/27 (`ما` over נשאר) · ezekiel/30/24 (a malformed flow). Each
  is one letter or one word of a neighbouring script inside otherwise
  sound Sorani. A Sorani ear's hand pass.
- **Aramaic** — daniel/3/12 `יתהון`, Aramaic's own object marker, glossed
  ⟨את⟩. Held fleet-wide pending the Aramaic marker ruling.
- **The marker classes** — 25 verses whose flow carries one ⟨את⟩ fewer
  than its rows; 22 whose flow carries a family form where the row has
  the bare marker. Reported, not cured.
- **For a native ear** — شابات vs شەممە · فەرموو vs وت · the remaining
  final-ه set (names and پادشاه) · the coined method terms. See
  [NOTES.md](NOTES.md).

No verse in this repository was hand-rendered.

## Final

**23,213 / 23,213 verses · 305,507 / 305,507 token rows.** یاهوە in
**6,828 of 6,828** Name seats — no title in the Name's place, no spelling
drift. Every structural census class zero except the declared marker
classes and the five stubborn seats.
