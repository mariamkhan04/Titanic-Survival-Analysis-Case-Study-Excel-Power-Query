# Titanic Passenger Survival Analysis — Insights Report

## Problem Statement

After the sinking of the Titanic, this project takes on the role of a data analytics
consultant investigating whether passenger survival was random or driven by identifiable,
structural factors. The analysis is built on a 1,309-passenger Titanic dataset
([source](https://www.kaggle.com/datasets/sakshisatre/titanic-dataset)) covering passenger
class, age, gender, fare, family composition, and port of embarkation. The objective is to
move beyond raw statistics and produce evidence-based, business-style conclusions suitable for
executive reporting: evaluating not just *what* happened, but *why* it likely happened, from
an access-to-resources and crisis-management-priority perspective.

**What makes this analysis different:** most public Titanic projects stop at surface-level
survival percentages. This project goes further by actively testing whether each pattern holds
up under scrutiny rather than taking it at face value, for example, catching that the apparent
"family boosts survival" effect is largely a gender-driven illusion once disaggregated (a
Simpson's Paradox check), and confirming that Cherbourg's higher survival rate is only partly
explained by its First Class-heavy passenger mix, with a real effect remaining even after
controlling for class. The dataset was also cleaned two independent ways, manually via
formulas and via Power Query, as a built-in accuracy cross-check. The result is a set of
insights that hold up to a follow-up "are you sure that's not just X?" question, which is the
standard a business stakeholder would actually apply.

## Executive Summary

Only 38% of passengers survived. Survival was not random, it followed two reinforcing
patterns: **economic status** (class and fare) and **evacuation priority** (gender and age).
First Class passengers survived at more than double the rate of Third Class, and women
survived at nearly four times the rate of men. Family status initially looked like an
independent driver, but disaggregating by gender shows it mattered only for men; for women,
survival was already high regardless of family status. Embarkation port also carries a small
independent effect beyond what class composition explains. Because all of these variables were
known before the ship ever sank, they could plausibly have powered a predictive risk model
ahead of departure.

## Key Business Questions

1. Was survival random, or were certain passenger segments more likely to survive?
2. Did socio-economic status influence survival chances?
3. Did age, gender, or family size affect survival, and did crisis management favor particular groups?
4. Could survival likelihood have been predicted before departure using available passenger data?

---

## Q1 — Was survival random, or were certain segments more likely to survive?

**Insight:** Survival was clearly not random. 62% of First Class passengers survived compared
with only 26% of Third Class passengers, while 73% of females survived compared with 19% of
males, a much wider gap than random chance would produce.

**Business reasoning:** These gaps point to two main drivers. First, class location mattered,
First Class passengers were closer to the upper decks and lifeboats, while Third Class
passengers were more spread out with less direct access. Second, evacuation priority mattered, women and children were given preference during boarding. Together, physical access and
crisis-management priorities explain the outcome, not random chance.

## Q2 — Did socio-economic status influence survival chances?

**Insight:** There was a strong association between economic status and survival. 62% of First
Class passengers survived, compared with 43% of Second Class and 26% of Third Class. High-fare
passengers also survived at 71%, compared with just 32% among low-fare passengers.

**Business reasoning:** Passenger class reflected differences in price paid, accommodation, and
location on the ship. So wealth may not have directly caused survival; instead, it was
connected to a set of advantages that could improve access to evacuation opportunities.

As a broader hypothesis worth exploring: in some systems, people seen as more economically or
strategically important may receive greater attention or priority during a crisis. This isn't
confirmed by this dataset alone, but it's a reasonable direction for further investigation
rather than a firm conclusion.

## Q3 — Did age, gender, or family size affect survival? Did crisis management favor particular groups?

**Insight:** Gender had the strongest link to survival: 73% of females survived vs. 19% of
males. Male children also survived far more (53%) than most adult male groups.

**Business reasoning:** This fits an evacuation approach that prioritized women and children
when lifeboat space was limited, gender and age shaped who got access.

**On family size:** "With family" passengers survived more overall (50% vs. 30% single), but
this gap almost disappears for females (73% vs. 72%) and only holds for males (16% vs. 26%).
So family presence didn't directly cause survival — it more likely reflects men traveling with
women/children being part of prioritized groups, plus families coordinating evacuation
differently than individuals.

## Q4 — Could survival have been predicted before departure?

**Insight:** Yes. Variables available before departure: class, gender, age, fare, family size,
and embarkation point, all showed clear differences in survival rates.

**Business reasoning:** These variables could have been used as features in a predictive model.
The model wouldn't know the outcome for certain, but it could estimate survival probability for
different passenger profiles based on their class, gender, age, and family composition. This
reflects standard BI/ML thinking: historical data → identify patterns → engineer features →
estimate probability → support decision-making.

---

## Additional Segment Insights

**Embarkation Port:** Cherbourg passengers survived most (55%), partly because more First Class
passengers boarded there; Cherbourg's passenger mix was 51.7% First Class vs. Southampton's
19.3%. But even within the same class, Cherbourg still outperforms Southampton (e.g. Third
Class: 37% vs. 21%), so port carries a small independent effect beyond what class composition
alone explains.

**Salutation (Title):** "Mrs" survived the most (79%), "Mr" the least (16%), this mainly
reflects the underlying gender split, with married/adult women prioritized and adult men not.

## Methodology 

- Source dataset: 1,309 passenger records.
- Raw data cleaned and transformed twice, independently: once using formulas/manual steps, and
  once using Power Query to cross-check consistency.
- Removed 4 rows with rare/nonsensical salutations (each occurring only once).
- Age: missing values imputed with the average age (30), then used to build Age Group.
- Fare: 1 missing value imputed with 0, placing it in the "Low" fare category (matching the
  mode).
- Embarked: 2 missing values imputed with the mode, Southampton.
- Derived fields created: Survived Category (Alive/Dead), Pclass Category, Salutation, Age
  Group, Family Size, Family Status, Fare Category, Embarked Category.
- Final cleaned dataset used as the pivot table source range; all pivot tables and dashboard
  visuals built from this single source of truth.

## Limitations & Assumptions

- Some segments have very small sample sizes (e.g. certain salutations like "Countess," "Sir,"
  "Lady" — n=1), so their individual rates are not statistically reliable and are treated as
  directional only.
- Embarkation port and class are correlated (a confound); the port effect reported above is net
  of a partial, not full, control for class.
- Age imputation (mean) introduces some uncertainty into age-based segments.
- This is an exploratory, correlation-based analysis — no formal statistical significance
  testing (e.g. chi-square) was applied, so relationships are described as associations, not
  proven causal effects.

## Conclusion

The evidence points to a clear conclusion: survival aboard the Titanic was not random. It was
shaped by two reinforcing systems: economic access (class and fare) and evacuation priority
(gender and age), with family status acting as a secondary, gender-dependent effect rather
than an independent driver. Because every predictive variable examined here was known before
the ship ever sank, this case demonstrates a broader principle directly relevant to modern
analytics work: pre-event data, properly segmented and stress-tested, can surface risk patterns
in advance of a crisis, turning historical analysis into a genuinely proactive decision-making
tool, not just a retrospective explanation.