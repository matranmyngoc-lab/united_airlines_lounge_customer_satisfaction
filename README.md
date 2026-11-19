# United Airlines Lounge Customer Satisfaction


How satisfied are United Airlines lounge customers, what is pulling that satisfaction down, and where should United spend first to improve? This project analyzes 125 United lounge reviews (2015–2025) against 2,936 reviews from 152 other airlines, using SQL for the metrics, Python for the priority matrix, and a dashboard for the story.

## Key takeaway

United's lounge rating is **close to other airlines** (3.11 vs 3.39). **Catering** is the lowest-rated category (2.54) and **bar and beverages** is next (2.91). Catering is also low at American and Delta, so it is a weak spot across the industry and a larger one at United. Recommended priority: catering first, bar and beverages second.

## Approach: from one number to seven

The measure I care about most is the **overall rating**, because it is the simplest way to say how satisfied customers are. But the overall rating is the average of up to **seven category scores** (comfort, cleanliness, bar and beverages, catering, washrooms, Wi-Fi and staff service), so one number cannot show how each category is doing. United's 3.11 hides a range from 3.70 (Wi-Fi) to 2.54 (catering). A strong category can mask a weak one.

So my analysis has two parts. First, it examines how the categories and services can be compared within the company, then compare those services to another airlines. 

To be more specific, it investigates the overall number and tests whether it is real. Second, it **breaks the rating into the average of each of the seven categories** to find what is driving it, then checks that finding over time and against other airlines.

| Step | Question | Charts |
|---|---|---|
| 1 | What is the overall number? | KPI Cards, Rating bands; rating comparison; recommendation comparison; rating band distribution |
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

**Business question:** Of the customers who review United's lounges, how many are happy, indifferent or unhappy? What are the overall rating for each category?

**Metric and why:** the share of reviews in each rating band (Good, Medium, Bad). An average alone can hide a split between very happy and very unhappy customers. Shares show how the ratings are distributed.

**What it shows:** 33.6% satisfied, 41.6% neutral, 24.8% dissatisfied. The most common outcome is neutral, and about one in four reviews is negative.


### Chart 1.2 Categories review count

**Business question:** How much can I trust each category average?

**Metric and why:** the number of reviews that scored each category, shown next to its average rating. Reviewers can skip categories, so each average rests on a different number of scores. A high or low average built on a few reviews can mislead, while one built on many is more reliable. The count tells me how much weight each average can carry. It also shows coverage: the share of the 125 United reviews that scored the category.

| Category | Average | Scores | Coverage | 95% margin |
|---|---|---|---|---|
| Wi-Fi | 3.70 | 117 | 94% | ±0.23 |
| Cleanliness | 3.38 | 124 | 99% | ±0.24 |
| Staff service | 3.17 | 121 | 97% | ±0.28 |
| Comfort | 3.15 | 125 | 100% | ±0.24 |
| Washrooms | 3.02 | 103 | 82% | ±0.28 |
| Bar and beverages | 2.91 | 113 | 90% | ±0.27 |
| Catering | 2.54 | 122 | 98% | ±0.27 |

**What it shows:** every category has more than 100 scores (103 to 125), so no average rests on a thin sample, and each is reliable to about ±0.25 points. 
- **Wi-Fi and catering are clearly different.** With 117 and 122 scores, the gap of 1.16 points is about 6.5 standard errors. Wi-Fi really is rated higher than catering.
- **Catering is clearly below the middle group.** It trails comfort by about 0.6 points, around 3 standard errors.
- **The middle categories can't be ranked.** Staff service (3.17) and comfort (3.15) differ by 0.01, and washrooms (3.02) and bar and beverages (2.91) by 0.11. Categories within about half a point of each other are statistically tied. Bar and beverages is only borderline below the others (about 1.9 standard errors from catering).

So the supported reading is three tiers: Wi-Fi (and probably cleanliness) clearly high, a middle group that can't be ordered, and catering clearly low.

**Caution:** the count shows how many reviewers scored a category, not whether the ones who skipped it differ from those who scored it. Washrooms was skipped by 18% of reviewers, so its average may be less representative than the others.

**Takeaway:** United's overall rating of 3.11 hides a wide spread across categories, from 3.70 for Wi-Fi to 2.54 for catering. Because every category has 100+ scores, that spread is reliable. Catering is the solid priority to improve. Bar and beverages is a lower-confidence second, since it isn't clearly worse than the middle group. 


### Chart 1.3 & 1.4:  Recommendation rate and Recommendation gap

**Business question:** Which categories separate customers who recommend the lounge from those who don't?

**Metric and why:** each category's average among recommenders (74 reviews) minus its average among non-recommenders (51 reviews). A low average shows where customers are unhappy. The gap shows how closely a category goes with recommending. Together they show where improvement is most likely to matter.

**What it shows:** catering is the lowest category for both groups (3.47 and 1.10), and 92% of non-recommenders rated it 2 or lower, so it is poor for happy and unhappy customers alike. Staff service has the largest gap (2.58), but each gap has a margin of about ±0.3, so it isn't clearly larger than catering, bar and beverages or comfort. Wi-Fi has the smallest gap (1.73) and is clearly less tied to recommending than staff service. Recommenders rate every category about 2 points higher, so this shows association, not which category causes a recommendation.

### Chart 1.3 Satisfaction vs recommendation rate over time

**Business question:** Is United's lounge satisfaction improving, and do rating and recommendation move together?

**Metric and why:** the yearly average overall rating and recommendation rate, with the number of reviews behind each year. A single overall average hides direction, so the trend shows whether satisfaction is rising, falling or flat. Showing the review count tells me how much each yearly point can be trusted.

**What it shows:** Both the satisfaction rating and the recommendation rate rise from 2015 to 2018, then fluctuate. The review counts show how much to trust each year: after 2019, every year has fewer than 10 reviews (1 to 9), so those yearly numbers are too thin to read, and the sharp drops and spikes (2020, 2021, 2025) are individual reviewers, not trends. 2015 is the most reliable year (45 reviews), with a 2.59 rating and 38% recommending. The 80 reviews from 2016–2025 average 3.40 and 71%, a clear improvement over 2015.

**Takeaway:** Lounge satisfaction is clearly better than in 2015, but there isn't enough data in recent years to say whether it kept rising or stayed flat. The supported message is "improved after 2015," not a continuous increase.


### Recommendation rate by airport

**Business question:** Do customers recommend United's lounges equally at every airport?

**Metric and why:** the recommendation rate by airport, with the number of reviews. Lounges differ by location, so an airport view shows whether the overall rate hides strong and weak locations. Only airports with at least 11 reviews are shown.

**What it shows:** Heathrow (93%, 14 reviews) and O'Hare (79%, 14) are clearly high. San Francisco (46%, 26) and Newark (36%, 11) are clearly low. Houston (64%, 11) can't be separated from the rest. With 11 to 26 reviews per airport, the margins are ±13 to ±28 points, so treat this as tiers, not a precise ranking.

### Category ratings by airport 

**Business question:** Is United's catering weakness specific to one airport, or does it show up everywhere?

**Metric and why:** the average of each of the seven categories at each airport, shown as a heatmap. It tests whether the category findings from Step 2 hold across locations.

**What it shows:** catering is the lowest category at four of the five airports and second-lowest at O'Hare, and it is below 2.5 at three of the four U.S. airports (San Francisco, Houston, Newark). Wi-Fi is the highest category at four of five. The overall ranking of airports matches the recommendation chart: Heathrow (4.41), O'Hare (3.75), Houston (3.23), San Francisco (2.80), Newark (2.57). Each cell rests on 11 to 26 scores, so only the broad pattern is reliable.

**Takeaway:** the catering weakness appears at almost every airport, and the biggest differences between locations are in overall lounge quality. San Francisco, with the most reviews (26), is the best-supported problem location. Heathrow's and O'Hare's reviews are mostly from 2015–2020 and 2015–2022, so check them against recent data.

### Lounge brand performance

**Business question:** Do United's lounge brands differ in customer satisfaction?

**Metric and why:** the average overall rating by brand (United Club, Polaris, other/unclassified), shown with the number of reviews behind each. Lounge names were standardized into United Club and Polaris. The review count shows how far each average can be trusted.

**What it shows:** Polaris is the highest rated (4.28, 12 reviews), about one point above United Club (3.29, 56 reviews). Other/unclassified is lowest (2.32, 57 reviews), but it is a catch-all of unnamed and unmatched lounges, including many First Class reviews, so it isn't a brand. Polaris has fewer than 20 reviews, all from business-class lounges since 2017, so brand can't be separated from lounge type or timing.

**Takeaway:** Polaris appears to be the best-liked lounge brand, but 46% of reviews have no usable brand and the Polaris sample is small, so this is a direction to check, not a conclusion.

### Chart 1.2 Average rating: United vs other airlines

**Business question:** How does United's overall lounge rating compare with other airlines?

**Metric and why:** the mean overall rating (the average of the seven category scores per review) for United against all other airlines combined. It is the primary satisfaction measure, and using all other airlines as the benchmark gives a large comparison base (2,936 reviews, 152 airlines).

**What it shows:** United is at 3.11 against 3.39, a gap of 0.28. With 125 United reviews the margin on United's rating is about ±0.22, so the gap is small but real.

### Recommendation rate: United vs other airlines

**Business question:** Would customers recommend United's lounges as often as they recommend other airlines' lounges?

**Metric and why:** the share of reviews where the customer would recommend the lounge. It measures a decision, so it checks whether the rating gap matters in practice.

**What it shows:** 59% against 64%. The 5-point gap is within the noise of a 125-review sample (about ±9 points), so there is no clear difference in recommendation.

**Takeaway:** United's overall rating is slightly lower than other airlines', but customers recommend United's lounges about as often. The small rating gap is why the analysis then looks at categories, time and lounge type for the source.
### Recommendation

Put the next lounge service spend on **catering first and bar and beverages second**. Catering is the lowest of seven categories, the lowest for both recommenders and non-recommenders, and below American and Delta. Keep Wi-Fi where it is. Look at staff service, cleanliness and washrooms next.

---

## Additional views (not part of the main flow)

**Business question:** Does the experience differ by airport or by lounge brand?

**Metric and why:** recommendation rate by airport, category ratings by airport (heatmap) and average rating by brand (United Club, Polaris, other). These test whether the findings hold across locations and products.

**What they show:** Heathrow has the highest recommendation rate (92.86%) and Newark the lowest (36.36%). Catering is rated below 2.5 at all six U.S. airports shown, which supports Step 2. Polaris (4.28) is rated above United Club (3.29). These cells have **fewer than 20 reviews** except United Club and unclassified, so they are directional only.




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



## Tools

- **SQL** (Mode) for metrics and aggregation
- **Python** (Jupyter, pandas, Matplotlib) for the priority matrix
- **Dashboard** for the full story

## Limitations

- **Small sample.** There are only 125 United reviews. 
- **Small groups.** Pay to Use, Unknown lounge type, individual airports and brands have too few reviews to support firm conclusions.
- **Big 3 comparison.** American and Delta have only 73 and 38 reviews, so those gaps should be treated as directional.
- **Self-selected reviews.** Online reviews over-represent customers with strong opinions, so compare relative gaps rather than reading absolute scores as the true average.
- **Association, not cause.** The recommendation gap shows which categories go with recommending a lounge, not what causes it.

## Author

Ngoc Ma
