# NOTES — selah-ckb, chair 96

*تێبینییەکانی کارکردن بە ئینگلیزی نووسراون — ئەوە زمانی کارکردنی ئەو
دیسیپلینەیە کە بەسەر هەموو کورسییەکاندا دەڕوات، و تێبینییەکان ئاماژە بە
مۆرفۆلۆژی و ژماردن و کۆدی شیکردنەوە دەکەن. بەڵگەنامەکانی ڕووەو خوێنەر —*
`README.md` *و* `CONTRIBUTING.md` *— بە سۆرانین، وەک پێویستە بۆ
بەڵگەنامەکانی خودی ئەم کورسییە. باسی تەواوی ئەوەی ڕوویدا لە*
`PROVENANCE.md` *دایە.*

Lit 2026-09-24. Burn complete the same day. Floor 23,213 verses ·
305,507 token rows.

Second Kurdish chair, beside Kurmanji — and the **first Kurdish chair in
the Perso-Arabic script**. Kurmanji sits in Latin (Hawar). Two standards,
two scripts, two readerships; neither chair serves the other's page. The
Name was carried over from Kurmanji's **Yahwe** letter for letter:
**یاهوە**.

---

## Burn signature

| | |
|---|---|
| relay | `batch/relay-move-on! [:ckb]`, engine-side |
| model · tier | `glm-5.3` · `glm-5.2`, every verse |
| after the relay | 23,197 / 23,213 — 16 tail batches timed out |
| gleaning | `translate-corpus-batched!`, batch 2 — all 16 landed |
| final | **23,213 / 23,213 verses · 305,507 / 305,507 token rows** |

## The thermometer

This chair is written with the same alphabet as Persian and Arabic, and
the model has seen far more of both than of Sorani. So the probe is
**script**, not vocabulary:

- the Arabic letters Sorani does not write — ث ذ ص ض ط ظ ة, and Arabic
  ك (U+0643) / ي (U+064A) for Sorani ک (U+06A9) / ی (U+06CC);
- final **ه** where Sorani writes **ە** (U+06D5) — the Persian tell;
- Persian and Arabic whole words (است, این, از, بود, گفت …), whitelist
  first, because Sorani's own words look Persian (بە, و, ئاسمان, زەوی,
  ئاو);
- **one Latin letter** outside ⟨ ⟩ — that is Kurmanji, this chair's
  sibling in the other script;
- ڕ and ڵ present, as a rate: their loss (ڕۆژ → روز, ساڵ → سال) is the
  chair sliding toward Persian.

Every class is read on **both surfaces** — the reader's flow and the
token row. The row carried more than the flow in every round.

## The Name

Sorani Bibles print **خواوەند**, **پەروەردگار**, **خودا**. This chair
writes **یاهوە**, and keeps the rest of the table: ئێلۆهیم · ئێل ·
ئێل شادای · ئادۆنای · یاه · سەڤائۆت · ئێهیێ ئەشێر ئێهیێ.

**Name seats reading یاهوە: 6,828 of 6,828.** No title stands in the
Name's place; no spelling drift.

**The repair that got there had to read the token, not the spelling.**
The first census found 193 seats drifted off یاهوە (یاهوو, یاهووم). A
dry run of a blind spelling repair caught what it would have broken:
**Jehu** (יהוא → یاهوو), **Jehoiakim** (یاهوویاکیم), and every *-yahu*
name (بێرێخیاهوو). The cure was re-written to key on the Hebrew token,
and then cured 22 surfaces on 20 seats and nothing else. Later rounds
re-cured the few the re-press brought back; the pass is idempotent.

## No hand-rendered verse

**No verse in this repository was written or spliced by hand.** Every
seat is machine-pressed under the rails. The repairs were deterministic
and mechanical — token-guided substitutions, the Arabic ك/ي to Sorani
ک/ی, and the restoration of Hebrew surfaces from the record — each one a
diff you can read in the git history. The hand pass this chair still
wants belongs to a Sorani ear, and it has not been taken.

## Open seats — declared, not repaired

| seat | what | waiting on |
|---|---|---|
| exodus/2/15 | `میدjan` — Latin inside Midian | a Sorani ear |
| nehemiah/5/13 | `لێdam` — Latin inside a Sorani word | a Sorani ear |
| hosea/3/5 | an IPA ɪ inside a Sorani word | a Sorani ear |
| exodus/8/27 | `ما` standing over נשאר — Arabic, not Sorani | a Sorani ear |
| ezekiel/30/24 | a malformed flow | a Sorani ear |
| daniel/3/12 | `יתהון` — Aramaic's own object marker, glossed ⟨את⟩ | the Aramaic marker ruling, held fleet-wide |

**These five survived all five re-press rounds.** They are the chair's
own signature: the burn residue on this chair leaned toward *one letter
of a neighbouring script inside an otherwise sound Sorani word* — the
same behaviour the thermometer was built for, arriving in the places a
whole-word probe cannot see.

### The marker gap

The flow and the rows do not always carry the same number of ⟨את⟩. The
curve across the rounds: **1,202 → 310 → 129 → 33 → 10**, and finally a
gap of **−15** — the flow now carries slightly *more* than the rows.
What stands:

- **25 verses** where the flow carries one ⟨את⟩ fewer than its rows.
  Inserting a marker into a flow is not safe by proof here, and the
  re-press did not settle them.
- **22 verses** where the flow carries a family form (⟨אתו⟩, ⟨מאת⟩)
  where the row has the bare ⟨את⟩. `marker_adjudicate` reports this
  class; it does not cure it.

## Held for a native ear

- **شابات vs شەممە** for שבת. Pinned **شابات** — a marked Hebrew word,
  because Sorani's everyday *شەممە* is the calendar's Saturday. If the
  everyday-word clause should win here, this flips.
- **فەرموو vs وت** for ויאמר. Sorani has an honorific *said*. Pinned:
  فەرموو for יהוה and for those the text honours, وت otherwise — a
  register distinction the Hebrew does not make (ויאמר is one verb). If
  this is theosemy the text does not license, it drops to وت everywhere.
- **Final ه for the eye.** After every round the remaining final-ه set
  is names and **پادشاه** (*king*). A Sorani reader should say which of
  these are the standard spelling and which are Persian.
- **میشکان** pinned for משכן, over a generic "tent of worship" — the
  same ruling as the Bulgarian chair's Мишкан.
- **1-kings/2/38** — אדני of a human king (Shimei to Solomon) reads
  `ئادۆنای ⟨خوای خودا⟩`. The rails say the Hebrew token decides, and
  here the token is a man's lord; both the transliteration and the
  supplied bracket look wrong. Noticed while these notes were written;
  not censused, not repaired.
- The coined method terms in the rails and the UI catalog — گەرماپێو
  (thermometer), ڕووەکە (surface), گلۆس (gloss), ڕەوانەکە (the flow).
