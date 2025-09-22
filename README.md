# Dataset Description

# 1. Movie Data from Daily Search in Date Range: 

## Each file in `daily_csvs/` corresponds to one day’s worth of search results on IMDB

## Dataset Schema

Each Row is for a unique movie

Columns are as follows:

| Column Name             | Type                 | Description                                                  |
|-------------------------|----------------------|--------------------------------------------------------------|
| `movie_link`            | `string`             | IMDb URL of the movie                                        |
| `movie_name`            | `string`             | Title of the movie                                           |
| `movie_poster_link`     | `string`             | Direct link to the movie poster image                        |
| `movie_year`            | `string`             | Year of the movie release                                    |
| `movie_time`            | `string`             | Duration in ISO 8601 (e.g. `PT1H30M`)                        |
| `movie_rating`          | `float`/`N/A`        | IMDb user rating value out of 10                             |
| `genre`                 | `list[string]`       | List of genres (e.g. `["Drama", "Romance"]`)                 |
| `short_description`     | `string`             | Brief synopsis or description                                |
| `how_many_people_rated` | `int`/`N/A`          | Total number of votes                                        |
| `movie_popularity_score`| `float`/`N/A`        | If movie in IMDB Most Popular, this is the ranking           |
| `director_name`         | `list[string]`       | Director name  list, max 3 directors, default None list      |
| `writer_name`           | `list[string]`       | Writer name list, max 5 writers, default None list           |
| `star_name`             | `list[string]`       | Star name list, default None list                            |
| `user_review`           | `int`                | Number of user reviews                                       |
| `critic_viewers`        | `string`/`N/A`       | Critic feedback, if present                                  |
| `meta_score`            | `int`/`N/A`          | Metacritic score, if present                                 |
| `wins_and_nominations`  | `dict`               | Wins and nominations count, defaults to 0                    |
| `oscar_link`            | `string`/`N/A`       | Link to first award event in movie's award page              |
| `top_cast_name_and_link`| `dict`/`0:0`         | For each top cast: name, link, character name, character link|
| `all_cast_crew_link`    | `string`             | Full credits link                                            |
| `more_like_movie_link`  | `dict`/`N/A`         | For each similar movie according to IMDB: name and link      |
| `aspect_ratio`          | `string`/`N/A`       | Aspect ratio of movie                                        |
| `sound_mix_company`     | `list[string]`       | Sound mix company and link                                   |
| `box_office`            | `dict`/`N/A`         | Box office details if available                              |
| `production_company`    | `list[string]`       | List of production companies                                 |
| `also_known_as`         | `string`/`N/A`       | Same movie known as other names, for e.g. in other language  |
| `language`              | `list[string]`/`N/A` | Movie language(s)                                            |
| `country_of_origin`     | `list[string]`/`N/A` | Movie's country of origin                                    |
| `release_date`          | `string`/`N/A`       | Release date in DD-MM-YYYY format, if no DD then raw string  |
| `faq_link`              | `string`             | Link of first FAQ question of movie                          |
| `user_review_link`      | `string`             | Link of all user reviews for movie                           |
| `facts_and_links`       | `dict`               | Did you know section of movie                                |
| `all_video_link`        | `string`             | Links to video media of movie                                |
| `all_photo_link`        | `list[string]`       | Links and titles of photo media of movie, max 50 per movie   |
| `filming_location_info` | `dict`               | Filming location, description and link if available          |
---

## Collection Details
- **Frequency**: Daily scrape per release date block
- **Scrape delay**: 2 seconds between requests to avoid rate limiting
- **Search filters**:
  - Runtime: `25–600` mins
  - Votes: `>= 50`
  - Title types: `feature, tv_movie, tv_special, documentary, tv_series, short, video, tv_short`
  - Sorted by: Release date (descending)

# 2. User Review Data for all movies scraped in "1. Movie Data from Daily Search in Date Range"
## Folder structure of `user_reviews/`

```
user_review/
├── Movie_Title_1/
│   ├── Movie_Title_1_page_1.csv
│   └── Movie_Title_1_page_2.csv
├── Movie_Title_2/
│   ├── Movie_Title_2_page_1.csv
│   └── Movie_Title_2_page_2.csv
├── ...
```
For each movie, if user reviews are available, then each page of user reviews is collected in sequential csv file

## Dataset Schema

Each row represents a user review for a specific movie on IMDb.

Columns are as follows:

| Column Name       | Type          | Description                                                         |
|-------------------|---------------|---------------------------------------------------------------------|
| `Review_number`   | `int`         | Sequential number of the review                                     |
| `User_rating`     | `string`      | Rating given by the user                                            |
| `Review_title`    | `string`      | Title of the user review                                            |
| `User_id`         | `string`      | Username or ID of the user providing the review                     |
| `User_id_link`    | `string`/`n/a`| Link to the user's profile (if available)                           |
| `Created_at`      | `string`      | Date when the review was extracted (DDs/MM/YYYY format)             |
| `Review_Text`     | `string`      | Full text content of the user review                                |
| `Spoiler`         | `bool`        | Flag indicating if the review contains spoilers (`True` or `False`) |
---

## Collection Details
- **Collection Method**: Automated scraping using Selenium WebDriver
- **Scrape Frequency**: Variable based on review load per movie
- **Scrape Delay**: 2 seconds between requests to avoid rate limiting

# 3. Movie Data from IMDB Top 250
## CSV in `top_250/` contains details of the top 250 movies on IMDB

## Dataset Schema 

Same as "1. Movie Data from Daily Search in Date Range"

# 4. MovieLens Latest Small 
## Dataset in `ml-latest-small/` contains links.csv, movies.csv, ratings.csv, and tags.csv

Ground Truth dataset for Ranking System of Movie Recommendation. 

This dataset (ml-latest-small) describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018. 

You can find further details in the ml-latest-small/README.txt

# Limitations & Notes

- `'N/A'` or None (blank) is used where values are missing.
- Some fields (like `meta_score` or `box_office`) may be sparsely populated.
- Photo files need to downloaded from links in `all_photo_link` in csvs from `daily_csvs/` and `top_250/`

# License / Use Disclaimer

This dataset is for **educational and research use only**.  
All data originates from [IMDb.com](https://www.imdb.com/), which owns the rights to its content.  
Do not republish or use for commercial purposes without complying with IMDb’s [Terms of Use](https://www.imdb.com/conditions).

