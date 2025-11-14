# Sample Test Dataset

This folder contains a trimmed, self‑contained slice of the Phase‑1 ranking test data. It has the exact same format as the hidden test dataset.  

Every rating record points to a movie that exists in the companion metadata
(`movie_mapper.csv`).

## File Inventory

| File | Rows | Users | Notes |
| --- | ---: | ---: | --- |
| `known_reviewers_known_movies.csv` | 1 495 | 39 | Reviewers already present in the AITH corpus (“known reviewers”) rated the “known movie” set. Each row keeps `user_name`, optional review text, rank, and `movie_link`. |
| `known_reviewers_unknown_movies.csv` | 438 | 22 | The same known reviewers above, but restricted to “unknown” titles. Columns: `user_name`, optional review text, rank, `movie_link`. |
| `unknown_reviewers_known_movies.csv` | 78 | 3 | Reviewers absent from the training data (“unknown reviewers”) evaluating the known movie set. |
| `movie_mapper.csv` | 433 | – | Metadata slice that matches the union of movie links referenced in the three rating CSVs. Columns mirror the canonical AITH scraping schema (plot synopsis, cast, links, etc.). |

## Quality Checklist

- **One‑to‑one alignment** – Every rating row references a movie that exists in
  `movie_mapper.csv`, so joins on `movie_link` are lossless.
- **Ranking** – Each user's highest rating corresponds to rank 1, and lowest rating corresponds to upper bound of the individual user's rankings. There can be multiple movies that have the same rank for an individual user.
- **Sampling** – Three cases are provided; grading is weighted, and the known–known case carries the highest share of marks. 

## Instructions
- **Working code** – We encourage you to focus on getting the end‑to‑end code working and learning from the data. Any fully working submission is welcome.
- **Number of Submissions** – We will take a total of max 5 submissions per team during the testing period. 

