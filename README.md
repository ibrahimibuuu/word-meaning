# Word Meaning — English Vocabulary Tracker

This repository stores the vocabulary list and quiz progress.

## Files
- `vocabulary.csv`: word list, Bengali meaning, English pronunciation in parentheses when available, attempts, correct answers, incorrect answers, and status.
- `quiz_history.csv`: per-question quiz history.

## Status rules
- `New`: not yet attempted.
- `Learning`: attempted but not yet consistently correct.
- `Mastered`: marked mastered after repeated correct recall; a single correct answer alone does not automatically prove long-term mastery.

## Quiz workflow
1. A quiz can focus on `New` words or mix new and previously studied words.
2. After the user answers, update Attempts and exactly one of Correct/Incorrect for each answered word.
3. Append each question and result to `quiz_history.csv`.
4. Add words from images with the English word unchanged, English pronunciation in parentheses, and Bengali meaning.

## Visibility note
This repository is public. Anyone may be able to view these learning records.

## Data note
The initial vocabulary import contains words recovered from the conversation context. Missing Bengali meanings/pronunciations and any unrecovered earlier words should be filled in when the original list or word images are available.
