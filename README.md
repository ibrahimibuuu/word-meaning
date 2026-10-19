# Word Meaning — English Vocabulary Tracker

This public repository stores the vocabulary list and the user's quiz progress.

## Files
- `vocabulary.csv`: one row per word with Bengali meaning, Attempts, Correct, Incorrect, and Status.

## Counting rules
For every word answered in a quiz:
- Increase `Attempts` by exactly 1.
- If the answer is correct, increase `Correct` by 1 and leave `Incorrect` unchanged.
- If the answer is wrong, increase `Incorrect` by 1 and leave `Correct` unchanged.
- Never reset previous totals when a word is answered again.
- Keep the invariant `Attempts = Correct + Incorrect` for words whose every attempt has been recorded.

Example: a word answered correctly twice and incorrectly once has Attempts=3, Correct=2, Incorrect=1.

## Status rules
Apply these rules after updating the counts, except for the legacy words described below:
- `New`: Attempts = 0; the word has not been attempted.
- `Mastered`: Attempts >= 5 and Correct / Attempts >= 0.80 (at least 80% correct).
- `Needs Practice`: Attempts >= 3 and Incorrect / Attempts >= 0.50 (at least half of attempts were incorrect), unless the word qualifies as Mastered.
- `Learning`: any attempted word that does not meet the Mastered or Needs Practice rule.

Check `Mastered` first, then `Needs Practice`, then `Learning`. The percentage is calculated from all recorded attempts, not just the latest quiz. Do not label an unattempted word as Mastered.

## Legacy status exception
The 56 words already marked `Mastered` at the time this policy was adopted retain their existing `Mastered` status. Do not recalculate those existing statuses just because they do not meet the new five-attempt threshold. If they are tested again, update their counts normally and preserve their Mastered status unless the user explicitly asks to re-evaluate legacy words. Newly learned words follow the rules above.

## Quiz/update workflow
1. Choose the requested quiz set (for example, New words only or a mix of New and reviewed words).
2. Ask the quiz and wait for the user's answers.
3. Grade each answer against the stored Bengali meaning / intended English word.
4. For every answered word, increment Attempts and exactly one of Correct or Incorrect.
5. Recalculate Status using the rules above, with the legacy exception.
6. Save the updated `vocabulary.csv` to the `main` branch and verify the resulting contents and counts.
7. Report the quiz score and the words whose counts/status changed.

## Adding words
When adding words from a picture or a supplied list, preserve each English word as written and include the pronunciation in parentheses when supplied or confirmed, plus its Bengali meaning. Avoid inventing missing meanings; ask if a word or meaning is unclear.

## Important: updates are not automatic
These CSV files are a record, not a running application. A quiz result does not change GitHub by itself. After a quiz, the assistant must grade the answers, update the CSV data, commit the changes, and verify the saved files.

## Visibility
This repository is public, so anyone may be able to view its contents. Do not store passwords or other sensitive information here.
