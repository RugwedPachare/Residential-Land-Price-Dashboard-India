# Residential Land Price Dashboard: India
An interactive Power BI dashboard, backed by a Python (pandas) cleaning notebook, that compares residential plot prices across 267 Indian cities and 22 states/UTs and shows how price per sq ft changes with plot size.
<img width="1451" height="807" alt="Screenshot 2026-10-16 194431" src="https://github.com/user-attachments/assets/4c10014f-d206-4e2d-9247-42f54a73cbe1" />

## Questions the project answers
+ Which cities, states and regions have the most expensive residential land per sq ft?
+ How does price per sq ft change as plots get larger?
+ Where are the listings concentrated?
+ Where do large plots (for example, sites big enough for a hotel or a small layout) cost the least per sq ft?

## Data
+ Source: a scraped snapshot of Indian property listings (data/real_estate_raw.csv): 269,418 rows covering apartments, floors, villas, houses and plots.
+ Scope used: the 47,624 rows labelled Residential Plot.
+ Fields: city, state, price (in lakh or crore), price per sq ft, area (sq ft).
+ Coverage note: the snapshot is not a random sample of India. Chennai and Hyderabad alone make up about a third of the plot listings, and some states (for example Gujarat) are absent. Findings describe this dataset, not the whole country.

## Data cleaning
+ Filtered to residential plots (269,418 rows down to 47,624).
+ Converted prices from text such as 90 L and 8.71 Cr to rupees (1 lakh = 100,000; 1 crore = 10,000,000).
+ Parsed 1,000 / sq ft into a numeric price-per-sq-ft column.
+ Trimmed whitespace in city names and standardised state names (for example maharastra to Maharashtra).
+ Mapped states to six regions (North, South, East, West, Central, Northeast).
+ Cross-checked price_inr against Area x price_per_area. 36 rows differed by more than 1%; they were kept and not corrected.
+ Removed 744 exact duplicate rows, leaving 46,880 listings.
+ Reviewed outliers (IQR rule and manual checks of very large areas and prices above ₹50,000 per sq ft). Outliers were kept, and the dashboard uses medians so they do not distort results.

## Dashboard
+ Slicers for region, state and plot-size segment.
+ Two adjustable cut-offs (what-if parameters) that define the segments: large plots (default 10,000 sq ft and above) and very large parcels (default 1 acre, 43,560 sq ft, and above).
+ KPI cards: listings, median price per sq ft, median plot price, acres on offer, and large-plot counts.
+ Charts: priciest cities, median price per sq ft by plot size segment, listings by state, and plot size versus price per sq ft (log scale).

## Key findings
+ The overall median is about ₹1,855 per sq ft, and the median plot is about 1,450 sq ft priced at roughly ₹27.6 lakh.
+ Delhi has the highest state-level median (about ₹13,500 per sq ft). West Bengal and Uttar Pradesh are among the lowest (about ₹1,040 to ₹1,090).
+ Among cities with 100+ listings, Gurgaon (about ₹11,700), Panchkula (about ₹7,500) and Rishikesh (about ₹5,600) follow Delhi.
+ By region, North has the highest median (about ₹2,070 per sq ft) and East the lowest (about ₹1,160).
+ Plot size and total price are positively related (Spearman 0.56), but price per sq ft does not fall steadily with size. Very large parcels are cheaper per sq ft, which fits with total price rising more slowly than area.
+ Among plots over 5,000 sq ft, cities such as Noida, Lucknow and Raipur have some of the lowest median prices per sq ft (about ₹380 to ₹800) in cities with at least 40 such listings.

## Limitations
+ Listing prices are asking prices, not sale prices.
+ Hotel- and township-scale are not in the data. The size segments are an assumption and the thresholds can be changed in the dashboard.
+ Very large parcels are a small sample (53 listings at 1 acre and above, before filtering).
+ Some prices per sq ft sit at exactly ₹100,000, which may be a platform cap or placeholder. These were left in.
+ Coverage is uneven across states and cities.

## Tools
Python (pandas, matplotlib), Jupyter, Power BI Desktop.

## Repository structure
data/        raw and cleaned CSV files
notebook/    cleaning and exploratory analysis
dashboard/   Power BI file (.pbix)
screenshots/ dashboard images
README.md

## Author
Rugwed Pachare
