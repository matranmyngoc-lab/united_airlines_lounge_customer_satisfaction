# United Airlines Lounge Customer Satisfaction


How satisfied are United Airlines lounge customers, what is pulling that satisfaction down, and where should United spend first to improve? This project analyzes 125 United lounge reviews (2015–2025) against 2,936 reviews from 152 other airlines, using SQL for the metrics, Python for the priority matrix, and a dashboard for the story.

## Key takeaway

United's lounge rating is **close to other airlines** (3.11 vs 3.39). **Catering** is the lowest-rated category (2.54) and **bar and beverages** is next (2.91). Catering is also low at American and Delta, so it is a weak spot across the industry and a larger one at United. Recommended priority: catering first, bar and beverages second.

## Approach: from one number to seven

The measure I care about most is the **overall rating**, because it is the simplest way to say how satisfied customers are. But the overall rating is the average of up to **seven category scores** (comfort, cleanliness, bar and beverages, catering, washrooms, Wi-Fi and staff service), so one number cannot show how each category is doing. United's 3.11 hides a range from 3.70 (Wi-Fi) to 2.54 (catering). A strong category can mask a weak one.

So the analysis does two things. First, it states the overall number and tests whether it is real. Second, it **breaks the rating into the average of each of the seven categories** to find what is driving it, then checks that finding over time and against other airlines.

| Step | Question | Charts |
|---|---|---|
| 1 | What is the overall number? | Rating bands; rating comparison; recommendation comparison; rating band distribution |
| 2 | Which of the seven categories pull it down? | Category averages; category review counts; recommendation gap |
| 3 | Is it rising or falling? | Satisfaction vs recommendation over time |
| 4 | Does it make sense next to others? | Rating and recommendation by lounge type; Big 3 comparison |
| 5 | What should be fixed first? | Service improvement priority matrix |

**Definitions used throughout**
- **Overall rating** = the mean of the category scores a reviewer filled in (1–5). Blank categories are left out of that review's mean.
- **Recommendation rate** = the share of reviews where the customer would recommend the lounge.
- **Satisfied / neutral / dissatisfied** = the Good / Medium / Bad rating bands.

---

## Step 1. What is the overall number?

### Chart 1.1 Rating bands (KPI cards)

**Business question:** Of the customers who review United's lounges, how many are happy, indifferent or unhappy?

**Metric and why:** the share of reviews in each rating band (Good, Medium, Bad). An average alone can hide a split between very happy and very unhappy customers. Shares show how the ratings are distributed.

**What it shows:** 33.6% satisfied, 41.6% neutral, 24.8% dissatisfied. The most common outcome is neutral, and about one in four reviews is negative.


### Chart 1.2 Average rating: United vs other airlines

**Business question:** How does United's overall lounge rating compare with other airlines?

**Metric and why:** the mean overall rating for United against all other airlines combined. It is the primary satisfaction measure and the one number that can be benchmarked directly. Using all other airlines as the benchmark gives a large comparison base (2,936 reviews, 152 airlines).

**What it shows:** United is at 3.11 against 3.39, a gap of 0.28. That is about 2.4 standard errors, so it is small but real.


### Chart 1.3 Recommendation rate: United vs other airlines

**Business question:** Would customers actually recommend United's lounges as often as they recommend other airlines' lounges?

**Metric and why:** the recommendation rate. It measures a customer decision, not a score, so it checks whether the rating gap means anything in practice.

**What it shows:** 59% against 64%. The 5-point gap is about 1.1 standard errors, which is within the noise of a 125-review sample. On the decision that matters, United is not clearly behind.


### Chart 1.4 Rating band distribution

**Business question:** Is the gap in the middle of the rating distribution or in the tails?

**Metric and why:** the share of reviews in each band for United and for other airlines, as 100% stacked bars. The mean can't say whether United has more unhappy customers or fewer happy ones. Stacked bands can.

**What it shows:** the middle is similar (about 42% medium for both). United has more Bad reviews (about 25% vs 16%) and fewer Good ones (about 34% vs 42%). The gap sits in the tails.




## Step 2. Which categories pull it down?

This is the step that matters most. The overall rating is a mean of seven scores, so I looked at the average of **each** category.

### Chart 2.1 Average rating by service category

**Business question:** Which of the seven categories pull the overall rating down?

**Metric and why:** the mean score of each category, sorted from highest to lowest. The overall rating is built from these seven, so taking it apart shows which parts drive it. The seven averages average about 3.12, close to the 3.11 overall (the small difference comes from blank scores).

| Category | United average |
|---|---|
| Wi-Fi | 3.70 |
| Cleanliness | 3.38 |
| Staff service | 3.17 |
| Comfort | 3.15 |
| Washrooms | 3.02 |
| Bar and beverages | 2.91 |
| Catering | 2.54 |

**What it shows:** catering (2.54) and bar and beverages (2.91) are the lowest, and Wi-Fi (3.70) the highest. The overall 3.11 hides a gap of more than a full point between the best and worst category.


### Chart 2.2 Categories review count

**Business question:** How many scores sit behind each category average, and how far can I trust it?

**Metric and why:** the number of non-blank scores per category. Reviewers can skip categories, so averages rest on different numbers of reviews.

**What it shows:** each category has 103 to 125 scores, enough to read the ranking, though not enough for small differences between neighbouring categories.


### Chart 2.3 Recommendation gap

**Business question:** Which categories separate customers who recommend the lounge from those who don't?

**Metric and why:** each category's average among recommenders minus its average among non-recommenders. A low average shows where customers are unhappy. The gap shows where being unhappy goes with not recommending. Together they point to what matters most.

**What it shows:** catering is the lowest for both groups (3.47 among recommenders, 1.10 among non-recommenders). Staff service has the largest gap, so staff interaction is the category most associated with whether a customer recommends. Wi-Fi has a relatively small gap. Recommenders rate every category higher, so this shows association, not cause.


## Step 3. Is it rising or falling?

### Chart 3.1 Satisfaction vs recommendation rate over time

**Business question:** Is lounge satisfaction improving, and do rating and recommendation move together?

**Metric and why:** the yearly average overall rating and yearly recommendation rate, drawn together. A single overall average hides direction. Showing two measures checks whether they tell the same story.

**What it shows:** both rose from 2015 to 2018, then fluctuated at a higher level than in 2015, and they move together. Each year after 2018 has 13 or fewer reviews, so individual year-to-year changes are not reliable.


## Step 4. Does it make sense next to others?

### Chart 4.1 Average rating by lounge type

**Business question:** Is United's gap concentrated in one type of lounge?

**Metric and why:** the average overall rating for United and for other airlines within each lounge type. Lounge types serve different customers, so a pooled gap can come from just one of them.

| Lounge type | United reviews | United | Others | Gap |
|---|---|---|---|---|
| Business Class | 48 | 3.29 | 3.35 | −0.06 |
| First Class | 26 | 2.51 | 3.61 | −1.10 |
| Frequent Flyer | 19 | 3.39 | 3.49 | −0.10 |
| Members | 16 | 3.68 | 3.52 | +0.16 |
| Pay to Use | 5 | 3.47 | 3.30 | +0.17 |
| Unknown | 11 | 2.23 | 3.17 | −0.94 |

**What it shows:** the gap sits in First Class and unknown-type lounges. Without those two groups, United is at 3.39 against 3.37 for others. Business Class, the largest group, is level with peers.



### Chart 4.2 Recommendation rate by lounge type

**Business question:** Do customers in each lounge type recommend United as often as they recommend others?

**Metric and why:** the recommendation rate by lounge type for United and others, shown next to review counts. It confirms the pattern in 4.1 on the decision measure.

**What it shows:** First Class (38% vs 68%) and unknown (18% vs 55%) trail clearly. Members (81% vs 66%) and Frequent Flyer (79% vs 70%) are ahead of peers, but with 16 and 19 reviews these are directional. Pay to Use has only 5 reviews and should not be read.


### Chart 4.3 Service rating vs American and Delta

**Business question:** Is each weak category a United problem, or weak across the industry?

**Metric and why:** the average of each of the seven categories for United, American and Delta (2015–2025). Putting the closest competitors next to United separates United-specific weaknesses from industry-wide ones.

| Category | United | American | Delta | United minus their average |
|---|---|---|---|---|
| Bar and beverages | 2.91 | 3.07 | 3.17 | −0.21 |
| Catering | 2.54 | 2.73 | 2.67 | −0.16 |
| Cleanliness | 3.38 | 3.76 | 3.70 | −0.35 |
| Comfort | 3.15 | 3.44 | 3.21 | −0.18 |
| Staff service | 3.17 | 3.59 | 3.42 | −0.34 |
| Washrooms | 3.02 | 3.30 | 3.41 | −0.34 |
| Wi-Fi | 3.70 | 3.82 | 3.81 | −0.12 |

**What it shows:** United is lowest in all seven categories. Catering is low at all three airlines, so it is partly an industry-wide weakness, and the gap is smaller against the Big 3 (−0.16) than against all other airlines. Cleanliness, staff service and washrooms each trail by about a third of a point. American and Delta have only 73 and 38 reviews, so treat these gaps as directional.

## Step 5. What should be fixed first?

### Chart 5.1 Service improvement priority matrix

**Business question:** Which categories should United improve first?

**Metric and why:** each category is placed by two measures: its average rating (x-axis, how weak it is) and its recommendation gap (y-axis, how closely it goes with recommending). A category that is both low and strongly tied to recommendation is the best place to spend. Built in Python with Matplotlib (see `notebooks/`).

**What it shows:** catering and bar and beverages land in the priority improvement quadrant. Staff service has the largest recommendation gap and needs a closer look. Wi-Fi has the highest rating and a small gap, so it should be maintained.



### Recommendation

Put the next lounge service spend on **catering first and bar and beverages second**. Catering is the lowest of seven categories, the lowest for both recommenders and non-recommenders, and below American and Delta. Keep Wi-Fi where it is. Look at staff service, cleanliness and washrooms next.

---

## Additional views (not part of the main flow)

**Business question:** Does the experience differ by airport or by lounge brand?

**Metric and why:** recommendation rate by airport, category ratings by airport (heatmap) and average rating by brand (United Club, Polaris, other). These test whether the findings hold across locations and products.

**What they show:** Heathrow has the highest recommendation rate (92.86%) and Newark the lowest (36.36%). Catering is rated below 2.5 at all six U.S. airports shown, which supports Step 2. Polaris (4.28) is rated above United Club (3.29). These cells have **fewer than 20 reviews** except United Club and unclassified, so they are directional only.


## Data

| File | Description |
|---|---|
| `airlines.csv` | Airline lookup (`airline_id`, `airline_name`) |
| `fct_lounge_reviews.csv` | One row per lounge review: airline, airport, recommended flag, verified flag, submission date, and seven category scores |
| `dim_lounges.csv` | [describe, e.g. lounge type and name by lounge] |

Source: [add source / link here].

- Reviews are filtered to **2015–2025**, and rows with an unresolved airline name (`"Read more"`) are excluded.
- Lounge name variations were standardized into **United Club** and **Polaris**; the rest are Other / Unclassified.

## Repository structure

```
.
├── sql/          # queries behind each dashboard chart
├── dataset/      # CSV results from running each query (same name as its .sql file)
├── notebooks/    # Python notebook for the service improvement priority matrix
├── images/       # notebook charts and dashboard screenshots
├── .gitignore
├── README.md
└── requirements.txt
```

Each file in `dataset/` is the output of the `sql/` file with the same name, for example `sql/03_category_recommendation_gap.sql` produces `dataset/03_category_recommendation_gap.csv`.

## How to reproduce

1. Run the queries in `sql/` against the review tables and save each result into `dataset/` under the same name.
2. Install the dependencies: `pip install -r requirements.txt`
3. Open the notebook in `notebooks/` and run it. It reads from `../dataset/` and saves charts to `../images/`.

## Tools

- **SQL** (Mode) for metrics and aggregation
- **Python** (Jupyter, pandas, Matplotlib) for the priority matrix
- **Dashboard** for the full story

## Limitations

- **Small sample.** There are only 125 United reviews. The rating gap is small but statistically real, and the recommendation gap is not distinguishable from zero.
- **Older reviews dominate.** About 78% of United's reviews are from 2015–2019 and only about 24 are from 2022–2025. The First Class finding rests mainly on 2015–2017 reviews (23 of 26), so it may not describe the current experience.
- **Small groups.** Pay to Use, Unknown lounge type, individual airports and brands have too few reviews to support firm conclusions.
- **Big 3 comparison.** American and Delta have only 73 and 38 reviews, so treat those gaps as directional.
- **Self-selected reviews.** Online reviews over-represent customers with strong opinions, so compare relative gaps rather than reading absolute scores as the true average.
- **Association, not cause.** The recommendation gap shows which categories go with recommending a lounge, not what causes it.

## Author

[Your name] · [LinkedIn / portfolio link]
