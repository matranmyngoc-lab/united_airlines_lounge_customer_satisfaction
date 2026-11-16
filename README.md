# United Airlines Lounge Customer Satisfaction

How satisfied are United Airlines lounge customers, what is pulling the rating down, and where should United spend first to improve? This project analyzes 125 United lounge reviews (2015–2025) against 2,936 reviews from 152 other airlines, using SQL for the metrics, Python for the priority plot, and a dashboard for the story.


## Key takeaway

United's lounge rating is **close to other airlines** (3.11 vs 3.39). **Catering** is the lowest-rated category (2.54) and **bar and beverages** is next (2.91). Catering is also low at American and Delta, so it is a weak spot across the industry and a larger one at United. Recommended priority: catering first, bar and beverages second.

## The thought flow

The dashboard follows one line of reasoning: state the headline number, break it down, check how it changes over time, then test it against others.

| Step | Question | Dashboard chart | Answer |
|---|---|---|---|
| 1 | What is the overall number? | KPI cards; avg rating and recommendation comparison; rating band distribution | 3.11 vs 3.39 for other airlines, a gap of 0.28. Recommendation 59% vs 64%, within the noise. |
| 2 | Which categories pull it down? | Average rating by service category; recommendation gap | Catering (2.54) and bar and beverages (2.91) are lowest. Wi-Fi is highest (3.70). |
| 3 | Is it rising or falling? | Service satisfaction vs recommendation rate over time | Rose from 2015 to 2018, then fluctuated at a higher level than 2015. |
| 4 | Does it make sense next to others? | Rating by lounge type; Big 3 service comparison | The gap sits in First Class and unknown-type lounges. Catering is low at American and Delta too. |

## Findings

### 1. Overall number

United averages **3.11** on 125 reviews; other airlines average **3.39**. The gap (0.28, about 2.4 standard errors) is small but real. The recommendation gap (59% vs 64%) is within the noise of a 125-review sample. United's rating bands are 33.6% satisfied, 41.6% neutral and 24.8% dissatisfied.


### 2. Categories

| Category | United average |
|---|---|
| Wi-Fi | 3.70 |
| Cleanliness | 3.38 |
| Staff service | 3.17 |
| Comfort | 3.15 |
| Washrooms | 3.02 |
| Bar and beverages | 2.91 |
| Catering | 2.54 |

Catering is the lowest category for both recommenders (3.47) and non-recommenders (1.10). Staff service has the largest recommendation gap, so staff interaction is the category most associated with whether a customer recommends the lounge. Recommenders rate every category higher, so this shows association, not cause.

![Category ratings](images/category_ratings.png)
![Recommendation gap](images/recommendation_gap.png)

### 3. Over time

United's rating and recommendation rate rose from 2015 to 2018, then fluctuated at a higher level than 2015. The two measures move together. Each year after 2018 has 13 or fewer reviews, so individual year-to-year changes are not reliable.

![Trend over time](images/trend_over_time.png)

### 4. Comparison with others

**By lounge type.** Business Class (48 reviews) is level with peers. The gap sits in First Class (−1.10, 26 reviews) and unknown-type lounges (−0.94, 11 reviews). Without those two groups, United is at 3.39 against 3.37 for others.

**Against American and Delta.** United is lowest in all seven categories. Wi-Fi is the smallest gap (−0.12). Catering is low at all three airlines (United 2.54, American 2.73, Delta 2.67), so the catering gap is smaller against the Big 3 (−0.16) than against all other airlines. Cleanliness, staff service and washrooms are each about a third of a point behind.

![Rating by lounge type](images/rating_by_lounge_type.png)
![Big 3 comparison](images/big3_comparison.png)

## Recommendation

Put the next lounge service spend on **catering first and bar and beverages second**. Catering is the lowest of seven categories, the lowest for both recommenders and non-recommenders, and below American and Delta. Keep Wi-Fi where it is. Look at staff service, cleanliness and washrooms next, since they trail the Big 3 by about a third of a point and staff service has the largest recommendation gap.

## Data and definitions

| File | Description |
|---|---|
| `airlines.csv` | Airline lookup (`airline_id`, `airline_name`) |
| `fct_lounge_reviews.csv` | One row per lounge review: airline, airport, recommended flag, verified flag, submission date, and seven category scores |
| `dim_lounges.csv` | [describe, e.g. lounge type and name by lounge] |

Source: [add source / link here].

- Reviews are filtered to **2015–2025**, and rows with an unresolved airline name (`"Read more"`) are excluded.
- **Overall rating** is the mean of a review's seven category scores, ignoring blanks.
- **Satisfied / neutral / dissatisfied** are the Good / Medium / Bad rating bands.
- **Recommendation gap** is a category's average among customers who recommended the lounge minus its average among those who did not.
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
- **Dashboard** for the full story; a PDF export is available on request

## Limitations

- **Small sample.** There are only 125 United reviews. The rating gap is small but statistically real, and the recommendation gap is not distinguishable from zero.
- **Older reviews dominate.** About 78% of United's reviews are from 2015–2019 and only about 24 are from 2022–2025. The First Class finding rests mainly on 2015–2017 reviews (23 of 26), so it may not describe the current experience.
- **Small groups.** Pay to Use, Unknown lounge type, individual airports and brands have too few reviews (under 20) to support firm conclusions.
- **Big 3 comparison.** American and Delta have only 73 and 38 reviews, so treat those gaps as directional.
- **Self-selected reviews.** Online reviews over-represent customers with strong opinions, so compare relative gaps rather than reading absolute scores as the true average.
- **Association, not cause.** The recommendation gap shows which categories go with recommending a lounge, not what causes it.

## Author

Ngoc Ma
