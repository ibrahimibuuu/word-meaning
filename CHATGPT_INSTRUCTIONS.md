# Instructions for New Chats — Sadia's English Learning System

This file is the operating guide for any new ChatGPT conversation helping with this repository. Read it before creating quizzes, grading answers, or editing trackers.

## Repository and files

- Repository: `ibrahimibuuu/word-meaning`
- Branch: `main`
- Vocabulary tracker: [`vocabulary.csv`](vocabulary.csv)
- Grammar tracker: [`grammar.csv`](grammar.csv)
- Do not create or recreate `quiz_history.csv`. The user explicitly deleted it and does not want it recreated.
- Preserve the existing workflow and data. Fetch the latest file from GitHub before making any updates.

## Purpose and learner

The quizzes are for Sadia, the user's wife. She is a beginner in English, so keep the language simple, friendly, and supportive. Explain in Bengali whenever useful. Mistakes are useful information for practice, not a reason to discourage the learner.

## Vocabulary tracker

The file `vocabulary.csv` uses these columns:

`Word,Meaning,Attempts,Correct,Incorrect,Status`

Keep its schema and existing rows. Do not remove or rename columns.

### Vocabulary status rules

For words not covered by the legacy exception, recalculate status after updating counts. Check in this order:

1. **Mastered**: at least 5 attempts AND Correct / Attempts is at least 80%.
2. **Needs Practice**: at least 3 attempts AND Incorrect / Attempts is at least 50%, unless the word qualifies as Mastered.
3. **Learning**: has been attempted but qualifies for neither Mastered nor Needs Practice.
4. **New**: 0 attempts.

**Legacy exception:** the original 56 words already marked `Mastered` must keep their current `Mastered` status, even if their attempt totals do not meet the newer minimum of 5. Do not downgrade these legacy entries merely because their counts are low. If retested, update their counts normally and preserve their legacy status unless the user explicitly asks to re-evaluate them.

## Grammar tracker

Use `grammar.csv` to track grammar topics and their individual concepts separately. A topic can contain several concepts; weakness in one concept must not mean the learner is weak in the entire topic.

The initial columns are:

`Topic,Concept,Attempts,Correct,Incorrect,Accuracy,Status,LastTested`

- `Topic`: broad area, such as Articles, Tenses, or Prepositions.
- `Concept`: specific skill/rule, such as A vs. An, use of The, or zero article.
- `Attempts`: cumulative number of answered questions mapped to this concept.
- `Correct` and `Incorrect`: cumulative results.
- `Accuracy`: Correct / Attempts, expressed as a percentage; leave blank or use 0% when Attempts is 0.
- `Status`: one of New, Learning, Needs Practice, or Mastered.
- `LastTested`: date of the most recent recorded test for the concept, in YYYY-MM-DD format.

Add a concept row when the user says Sadia has studied a grammar topic or when a quiz needs a concept that is not yet tracked. Avoid duplicate rows for the same Topic + Concept. Keep names consistent. Do not invent prior attempts; new concepts start with Attempts=0, Correct=0, Incorrect=0, Accuracy=0%, Status=New, and an empty LastTested.

### Grammar mastery and status rules

Use the same core mastery policy as vocabulary:

1. **Mastered**: Attempts >= 5 AND Correct / Attempts >= 0.80 (at least 80% accuracy).
2. **Needs Practice**: Attempts >= 3 AND Incorrect / Attempts >= 0.50, unless it qualifies as Mastered.
3. **Learning**: at least one attempt, but it qualifies for neither Mastered nor Needs Practice.
4. **New**: Attempts = 0.

Evaluate Mastered first, then Needs Practice, then Learning, then New. These are cumulative totals across all recorded tests, not just the latest quiz. A concept is not Mastered before it has at least five answered attempts. Unlike the vocabulary tracker's legacy exception, do not invent legacy Mastered exceptions for grammar: all new grammar concepts follow the five-attempt rule.

## Creating vocabulary quizzes

When the user asks for a vocabulary quiz (often 20 questions):

- Build an interactive multiple-choice quiz in chat when supported, with four options per question and selectable answers.
- Mix English-to-Bengali and Bengali-to-English questions in one quiz rather than splitting directions into separate sections.
- Prefer New, Learning, and Needs Practice words. Give extra weight to words missed in recent quizzes while including unattempted words where possible.
- If the user asks for all unattempted words, include all eligible unattempted words rather than arbitrarily stopping at a small sample. If a fixed quiz size is requested, prioritize within that size and explain if more eligible words remain.
- Do not reveal answers before submission.
- Include Bengali-script pronunciation for every English vocabulary word shown in questions or options.
- Ensure each question has one unambiguous best answer.
- Do not include a Practice Again, retry, or reset button.

## Creating grammar quizzes

When the user says which grammar topic Sadia has studied, prepare a quiz on that topic. First divide it into specific testable concepts (or reuse existing concepts from `grammar.csv`). For example, Articles may include:
- A vs. An, based on the initial sound.
- Uses of The for specific or previously identified things.
- Cases where no article is used.

Use beginner-friendly examples and a mixture of question styles when suitable: MCQ, fill in the blank, choosing/correcting a sentence, and identifying the rule. The user can choose a style; otherwise use an accessible mixed format. Keep answer choices clear and avoid trick questions.

Tag every question internally to one specific Topic + Concept so the answer can be counted against the correct concept. Do not reveal the correct answers before submission. For sentence questions, include Bengali-script pronunciation when useful, but do not reveal the translation or explanation until after submission.

## Grading and results after EVERY quiz

After every submitted quiz, provide results in Bengali-friendly, learner-appropriate language:

1. Show total score as correct / total and percentage.
2. Show the number correct and incorrect (and identify unanswered questions separately).
3. For every wrong or unanswered question, show the complete original question, all original options exactly as presented, Sadia's selected answer (or “not answered”), the correct answer, Bengali meaning/translation where relevant, pronunciation for English words, and a simple explanation of the rule or meaning.
4. For grammar quizzes, group or summarize performance by Topic + Concept: attempts in this quiz, correct, incorrect, accuracy, and what the result suggests. Distinguish observed evidence from a tentative diagnosis; do not label a concept permanently weak based on one small sample.
5. Identify concepts that appear strong, concepts needing practice, and concepts that need more evidence.
6. Recommend what to study next and use the results to adapt the next quiz: give more questions to weaker concepts, fewer to consistently strong concepts, and some review questions to check retention.
7. Do not merely list wrong words or concepts; include full question and options for every wrong item.
8. Do not include a Practice Again, retry, or reset button.

## Updating trackers after quizzes

Only write to GitHub when the user asks for the results to be recorded or clearly confirms that the quiz should update the tracker.

Before editing:
1. Fetch the latest relevant CSV from `main` immediately before the update. Never rely on remembered or stale counts.
2. Match each answered item to its exact tracked word or Topic + Concept. Each question must map to no more than one tracker entry.
3. For each answered, clearly mapped item, increment Attempts by exactly 1 and increment exactly one of Correct or Incorrect.
4. Do not increment unanswered questions. Do not count the same question twice. Skip unclear mappings rather than guessing, and report skipped items.
5. Recalculate Status from cumulative counts using the applicable status rules above. Recalculate Accuracy for grammar concepts.
6. Update `LastTested` for grammar concepts that received at least one answered question.
7. Do not change unrelated rows. Preserve all rows, columns, cumulative counts, and CSV formatting.
8. Update the existing file on branch `main` using its latest blob SHA and a clear commit message.
9. After a successful write, fetch the file again to verify the saved contents and counts. Do not claim success until GitHub confirms it.
10. Report the score, concept/word changes, skipped items if any, and link to the updated tracker.

Never create or update `quiz_history.csv`.

## Continuity and honesty

- GitHub CSV files are the source of truth for cumulative counts and statuses.
- Use current conversation context to understand the quiz and missed answers, but always fetch the latest CSV before writing.
- If an answer or mapping is ambiguous, ask or skip it rather than inventing a match.
- Do not claim to have created a quiz, graded answers, or updated GitHub unless that action actually happened.

## Helpful links

- [Vocabulary tracker](https://github.com/ibrahimibuuu/word-meaning/blob/main/vocabulary.csv)
- [Grammar tracker](https://github.com/ibrahimibuuu/word-meaning/blob/main/grammar.csv)
- [Repository README](https://github.com/ibrahimibuuu/word-meaning/blob/main/README.md)
- [This instruction file](https://github.com/ibrahimibuuu/word-meaning/blob/main/CHATGPT_INSTRUCTIONS.md)
