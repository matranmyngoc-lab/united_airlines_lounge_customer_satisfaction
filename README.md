# United Airlines Lounge Customer Satisfaction Analysis

An analysis of airport lounge reviews (2015–2025) to understand how satisfied United Airlines lounge customers are, which service areas hold the rating back, and how United compares with other airlines.

## Business question

How satisfied are United Airlines lounge customers, what is driving that satisfaction, and are there service areas United should prioritize to improve?

## Key takeaway

United's lounge satisfaction is close to other airlines overal: a small rating gap (−0.28 points) and no meaningful difference in recommendation rate. **Catering** Bar & **Beverages** are the lowest-rated categories and the largest gaps versus peers, making them the priority areas to improve, with catering the clearer case.

## Headline results

| Metric | United | Other airlines |
|---|---|---|
| Reviews | 125 | 2,936 (152 airlines) |
| Average rating (1–5) | 3.11 | 3.39 |
| Recommendation rate | 59% | 64% |

- **Rating bands (United):** 33.6% satisfied, 41.6% neutral, 24.8% dissatisfied.
- **Highest-rated category:** Wi-Fi (3.7). **Lowest:** Catering (2.54), then Bar & Beverages (2.91).
- **Largest recommendation gap:** Staff Service, so staff interaction is the category most associated with whether a customer recommends the lounge.
- **Versus American and Delta:** catering is low across all three airlines (United 2.54, American 2.73, Delta 2.67), so it is partly an industry-wide weakness rather than only a United one.
- **By lounge type:** Business Class, Frequent Flyer and Members lounges perform in line with peers. First Class lounges stand out (United 2.51 vs 3.61 for others, 26 reviews).
- **By brand:** Polaris (4.28) is rated higher than United Club (3.29).

## Analysis approach

The dashboard follows one line of reasoning:

1. **Headline number:** overall average rating and recommendation rate.
2. **Why that number:** service categories (which pull the rating down) and the recommendation gap between recommenders and non-recommenders.
3. **Over time:** when ratings are highest and whether they are rising or falling.
4. **In context:** comparison with all other airlines, by lounge type, and against the "Big 3" (American, Delta), to check whether the number makes sense.
5. **Action:** a service improvement priority matrix that places each category by average rating and recommendation gap.


### Cleaning and definitions

- Reviews are filtered to those submitted **2015–2025**.
- Rows where the airline name is unresolved (`"Read more"`) are excluded.
- **Overall rating** = the average of a review's seven category scores, ignoring missing scores.
- **Satisfied / neutral / dissatisfied** correspond to the Good / Medium / Bad rating bands.
- **Recommendation gap** (priority matrix) = a category's average score among customers who recommended the lounge minus its average among those who did not.
- Lounge name variations were standardized into **United Club** and **Polaris**; the rest are labeled Other / Unclassified.

## Tools
- **SQL** for aggregation and metric definitions
- **Python** (Jupyter notebook) and **Matplotlib** for the Service Improvement Priority Matrix (quadrant plot) 
- **Mode Analytics** built dashboard from SQL Queries 

## Repository structure

```
.
├── README.md
├── data/
│   ├── airlines.csv
│   ├── fct_lounge_reviews.csv
│   └── dim_lounges.csv
├── sql/
│   └── (queries for each dashboard chart)
├── notebooks/
│   └── (code for quadrant plot)
└── dashboard/
    └── united-airlines-lounge-customer-satisfaction.pdf
```
[Ngoc Ma]([https://www.linkedin.com/in/ngocmamanda/])
