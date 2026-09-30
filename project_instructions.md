# ECE big data processing project

## Project due date

Projects for all groups are due no later than **end of day November 15, 2026.**

## General guidelines

### AI & LLM policy

-**Coding:** AI/LLM usage is allowed for coding tasks but must be explicitly declared, including which tools were used.
-**Reporting and Reasoning Questions:** AI tools are strictly prohibited for answering any part of the project report or reasoning questions.
-**Violation Policy:** Unauthorized or undisclosed use of AI will result in a [X]-point deduction per question or occurrence.

### Git & Collaboration Workflow

-**Repository:** All projects will be submitted via a shared Git repository for the project.
-**Git standards:** Files must be committed and pushed using standard Git workflows. Direct uploading of files via the web interface is prohibited; non-compliant submissions will not be graded (or: will incur a penalty).
-**Pull/Merge Requests(MRs):**

  - Each unique question or task must be developed in a separate branch and submitted via an individual MR. **Note:** It is permitted to group related tasks in a single MR but not required. 
  - Every MR must be reviewed and approved by at least one other group member before merging.

-**Contribution Balance:** Students will also be evaluated on Git history and MR discussions. Each group member is expected to demonstrate roughly equal activity, assessed by both quality of commits and meaningful participation in peer code reviews.  

### Submission & Late Policy

-**General Rule:** Projects are expected to be submitted on or prior to **end of day, Sunday November 15, 2026.**
-**Exceptions:** If unforeseen circumstances arise, late submissions must be approved by the instructor prior no later than **Friday November 13, 2026.**
-**Late Penalty:** Unapproved late submissions will incur a 1-point deduction for each day past the initial due date.

### Required tools

-**Spark:** Required for all analytical and streaming data processing tasks.
-**Kafka:** Required for data ingestion and movement, serving as the stream source that ingests and feeds data into Apache Spark for processing.

## Questions/Instructions

### Data preparation 

- For each column of each table in the IMDB dataset, calculate the percentage of nulls, missing, or empty records.
  - Which five columns across the entire dataset have the highest percentage of null values ?
- Identify other data quality issues for the dataset such as principals who died before they were born, foreign keys with missing parent records, etc. 
- Design and implement a way to handle these values and explain why you chose this design/implementation. 

### Data exploration

- Identify all feature-length movies by genre whose length is notably different than the average length of movies in that genre.
- Identify the top three most popular movie genres for each year between 1980 and 2025. 
  - How do the top three genres compare to the rest of the genres of movies in a given year ?
- Find all directors who have directed exactly one movie with a rating >= 8.0 but who have multiple other movies directed with an average rating of <= 6.0. 
- Identify television series with at least three seasons consisting of >=10 episodes where the worst episode occurred in the last season and the best episode occurred within the first two seasons. 
- Find any actors/actresses who have achieved success across films in multiple distinct languages (e.g. been in a successful film originally in French and English). Additionally, list all actors/actresses who have achieved success in movies in >=3 languages (e.g. French, German, and English).
- Find all actors/actresses who have been in movies for 20+ years and at least 15 or more movies whose popularity peaked early in their career (e.g. had their highest rated movies early in their career as compared to later.) 
- Identify film professionals who can be considered "multi-talented" (e.g. some combo of writer/director/actor). How do these individuals perform when performing multiple roles on the same project (e.g. directing and acting in the same movie.)

### Data enrichment 

For all feature-length films released between 1980 and 2025, enrich the dataset by including a film synopsis for each of the top 10 films per genre for each year and biographical information for at least three principals from each film.  

- **Data Origin Rules:** All information must come from human-authored open sources such as Wikipedia or open-license movie databases. Machine generated text is strictly prohibited.
- **Provenance & Ethics:** The pipeline must respect target domain API rate limits and all other scraping policies and every enriched record must maintain an explicit lineage field citing its source URL/URI.
- **Engine Requirements:** Data gathering can be done outside of Spark but all other operations such as cleaning, schema enforcement, etc, must be performed using Spark.
- **Single-source Option:** Pipelines are not expected to hit multiple sources. For instance, if Wikipedia is used as the source and a film does not have a wiki page, it is not required to search a secondary source. However, it is expected that the majority of the information should be filled in and notes added when information is not currently available. 

### Streaming data processing

Design and implement a PySpark Structured Streaming pipeline that ingests live Wikipedia change events via Kafka and identifies updates relevant to your IMDb dataset. You may define your own strategy for filtering or subsetting the incoming stream (e.g., matching entity IDs, title broad-matching, language edition filtering, or category/namespace criteria), but your filtering criteria must be sufficiently broad to guarantee that multiple matching events are captured and processed within an $X$-minute test window (e.g., 15–30 minutes).
