# Instructions for New Chats — Sadia's English Vocabulary Learning System

This file is the operating guide for any new ChatGPT conversation helping with this repository. Read it before creating quizzes, grading answers, or editing the vocabulary tracker.

## Repository

- Repository: `ibrahimibuuu/word-meaning`
- Branch: `main`
- Vocabulary tracker: [`vocabulary.csv`](vocabulary.csv)
- Public tracker URL: https://github.com/ibrahimibuuu/word-meaning/blob/main/vocabulary.csv
- README: [`README.md`](README.md)
- Do not create or recreate `quiz_history.csv`. The user explicitly deleted it and does not want it recreated.

## Purpose and learner

The quizzes are for Sadia, the user's wife. She is a beginner in English, so keep the language simple, friendly, and supportive. Explain in Bengali whenever useful. Do not make the learner feel bad for mistakes; mistakes are useful information for practice.

## Vocabulary CSV format

The file `vocabulary.csv` uses these columns:

`Word,Meaning,Attempts,Correct,Incorrect,Status`

Meanings are generally in Bengali. Keep the existing schema and rows. Do not remove or rename columns.

## Status rules

Use these rules when recalculating status for words that are not covered by the legacy exception below. Check in this order:

1. **Mastered**: at least 5 attempts AND correct/attempts is at least 80%.
2. **Needs Practice**: at least 3 attempts AND incorrect/attempts is at least 50%, unless the word qualifies as Mastered.
3. **Learning**: has been attempted but qualifies for neither Mastered nor Needs Practice.
4. **New**: 0 attempts.

**Legacy exception:** the original 56 words already marked `Mastered` must keep their current `Mastered` status, even if their attempt totals do not meet the newer minimum of 5. Do not downgrade these legacy entries merely because their counts are low.

## Creating a quiz

When the user asks for another quiz (often 20 questions):

- Build an interactive multiple-choice quiz in the chat when supported.
- Use four options per question. Sadia should be able to select an option and submit answers.
- Mix question directions and question types throughout one quiz; do not split into separate English-to-Bengali and Bengali-to-English sections:
  - English word → choose its Bengali meaning.
  - Bengali meaning → choose the English word.
  - Simple English sentence → choose its Bengali meaning, or a simple Bengali prompt → choose an English sentence when appropriate.
- Prefer words marked `New`, `Learning`, or `Needs Practice`; do not spend most of the quiz on already-mastered words.
- Give extra weight to words missed in recent quizzes, while still including unattempted words where possible. Recent missed words have included: `crashes`, `wind`, `oasis`, `pilot`, `narrow`, `nodded`, and `status`. Check the current tracker and recent conversation context rather than treating this list as permanent.
- If the user asks for all unattempted words, include all eligible unattempted words rather than arbitrarily stopping at a small sample. If the requested quiz size is fixed, prioritize within that size and explain if there are more words remaining.
- Do not reveal the correct answers before the learner submits the quiz.
- Include Bengali-script pronunciation for every English vocabulary word shown in the question or answer options. Keep options readable, for example: `oasis (ওয়েসিস)`.
- For sentence questions, show the English sentence and its Bengali-script pronunciation, but do not show the sentence translation before the answer is submitted.
- Make distractors plausible but not confusingly ambiguous. Ensure there is one best correct answer.

## Grading and results

After the learner submits the quiz:

1. Show the score as `correct / total` and a percentage.
2. Show all wrong or unanswered questions in full. For **each** one, include:
   - The complete original question/prompt.
   - All four original options, exactly as presented, including Bengali pronunciation for English words.
   - The learner's selected option (or “not answered”).
   - The correct option and answer.
   - A simple Bengali explanation.
3. For sentence questions, include the full Bengali translation after grading and explain important words in Bengali.
4. Briefly summarize what to practice next.
5. Do not show only a list of wrong words; the user specifically wants the full question and every option for every incorrect question.

## Updating the vocabulary tracker after a quiz

Only update the repository when the user asks to update it or clearly confirms that the quiz results should be recorded.

Before editing:

1. Fetch the current `vocabulary.csv` from the repository's `main` branch immediately before making changes. Never rely on an old copy or remembered counts.
2. Match each answered quiz item to an exact tracked vocabulary word where possible.
3. For each clearly matched tracked word that was answered:
   - Increase `Attempts` by 1.
   - If correct, increase `Correct` by 1.
   - If incorrect, increase `Incorrect` by 1.
   - Recalculate `Status` using the rules above, preserving the legacy Mastered exception.
4. Do not increment unanswered questions.
5. Do not change unrelated words.
6. If a sentence question does not map clearly to a tracked vocabulary word, skip it rather than guessing. Mention skipped/ambiguous items in the results.
7. Preserve all rows and CSV formatting. Do not reset cumulative counts.
8. Use the GitHub file update action with the latest fetched blob SHA, on branch `main`, and a clear commit message.
9. After the write succeeds, fetch the updated file again to verify the change. Do not claim an update succeeded until GitHub confirms it.

Never create or update `quiz_history.csv`.

## Continuity and honesty

- The repository CSV is the source of truth for current vocabulary counts and statuses.
- Recent conversation context can help identify the latest quiz and missed words, but always fetch the CSV before writing.
- If an exact word, answer, or mapping is ambiguous, ask or skip it rather than inventing a match.
- Clearly report what was updated, what was skipped, the commit result, and the tracker link.
- Do not claim to have created a quiz, graded an answer, or updated GitHub unless that action actually happened.

## Helpful links

- [Vocabulary tracker](https://github.com/ibrahimibuuu/word-meaning/blob/main/vocabulary.csv)
- [Repository README](https://github.com/ibrahimibuuu/word-meaning/blob/main/README.md)
- [This instruction file](https://github.com/ibrahimibuuu/word-meaning/blob/main/CHATGPT_INSTRUCTIONS.md)
