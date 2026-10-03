# Digital Marketing Campaign Analysis

A Power BI dashboard exploring advertising spend, campaign performance, customer demographics, and engagement metrics.

## Project Overview

This project analyses digital marketing data to compare campaign channels and campaign types. It brings together advertising expenditure, average click-through rates, average conversion rates, and customer demographics in a single report.

The dashboard supports exploratory analysis of marketing performance and helps identify areas for further investigation.

## Dashboard Preview

![Digital Marketing Campaign Dashboard](screenshort%201.jpeg)

## Business Objectives

- Compare advertising expenditure across marketing channels.
- Examine average click-through and conversion rates.
- Analyse spending across campaign types.
- Explore customer distribution by gender.
- Monitor website, email, and customer engagement metrics.
- Identify opportunities for further campaign evaluation.

## Tools and Technologies

| Tool | Purpose |
|---|---|
| Power BI Desktop | Data modelling and dashboard development |
| Power Query | CSV import, header promotion, and data type conversion |
| DAX | Calculation of analytical measures |
| CSV | Source dataset format |

## Dataset Structure

The model contains the `digital_marketing_campaign_dataset` table with 20 fields.

| Area | Fields |
|---|---|
| Customer profile | CustomerID, Age, Gender, Income |
| Campaign details | CampaignChannel, CampaignType, AdvertisingPlatform, AdvertisingTool |
| Advertising performance | AdSpend, ClickThroughRate, ConversionRate, Conversion |
| Website engagement | WebsiteVisits, PagesPerVisit, TimeOnSite |
| Social and email engagement | SocialShares, EmailOpens, EmailClicks |
| Customer history | PreviousPurchases, LoyaltyPoints |

The source dataset's provenance, reporting period, and record-level definition are not documented in the repository.

## Dashboard Components

- Total advertising spend.
- Channel-level average conversion rate, average CTR, and advertising spend.
- Campaign-type average conversion rate, average CTR, and advertising spend.
- Customer count by gender.
- Advertising spend by campaign type.
- Advertising spend and customer count by campaign channel.
- Website, email, age, and loyalty metric panels.

Some KPI values are not visible in the uploaded screenshot and are therefore not reported below.

## Key Findings

### 1. Total Advertising Spend

The dashboard displays approximately **$40.0M** in total advertising spend.

This represents the sum of the `AdSpend` field. Its interpretation depends on the source data's record-level definition.

### 2. Performance by Campaign Channel

| Channel | Average Conversion Rate | Average CTR | Ad Spend |
|---|---:|---:|---:|
| Referral | 10.3% | 15.2% | $8,653,519 |
| SEO | 10.4% | 15.3% | $7,740,904 |
| PPC | 10.4% | 15.8% | $8,199,237 |
| Email | 10.5% | 15.6% | $7,871,576 |
| Social Media | 10.7% | 15.6% | $7,542,323 |

Based on the displayed values:

- **Referral** has the highest advertising spend.
- **Social Media** has the highest average conversion rate and the lowest spend among the listed channels.
- **PPC** has the highest average click-through rate.

These comparisons do not establish return on investment or cost efficiency. Conversion counts, revenue, and consistent measurement definitions are needed for those conclusions.

### 3. Performance by Campaign Type

| Campaign Type | Average Conversion Rate | Average CTR | Ad Spend |
|---|---:|---:|---:|
| Retention | 10.3% | 15.6% | $9,768,362 |
| Awareness | 10.4% | 15.6% | $10,077,846 |
| Conversion | 10.5% | 15.6% | $10,300,077 |
| Consideration | 10.5% | 15.2% | $9,861,274 |

Conversion campaigns receive the highest displayed expenditure. Conversion and Consideration campaigns share the highest displayed average conversion rate at **10.5%**.

Differences should be interpreted alongside each campaign type's objective rather than using conversion rate alone.

### 4. Customer Demographics

The gender chart displays approximately **4.84K female customer records**, exceeding the displayed male count.

The current Customer Count measure counts nonblank customer IDs. It does not verify that each customer is unique.

> Findings are based on the uploaded dashboard screenshot. Rates and displayed totals are rounded, and the source CSV has not been independently validated.

## DAX Measures

The following measures are included in the Power BI template.

### Email Click-to-Open Calculation

```dax
Email CTR% =
DIVIDE(
    SUM(digital_marketing_campaign_dataset[EmailClicks]),
    SUM(digital_marketing_campaign_dataset[EmailOpens]),
    0
) * 100
```

Because the denominator is email opens, this measure represents a **click-to-open calculation** rather than a click-through rate based on delivered emails.

### Average Click-Through Rate

```dax
Average CTR% =
AVERAGE(
    digital_marketing_campaign_dataset[ClickThroughRate]
)
```

### Average Pages per Visit

```dax
Average Page Visitor =
AVERAGE(
    digital_marketing_campaign_dataset[PagesPerVisit]
)
```

### Average Conversion Rate

```dax
Average Conversion Rate =
AVERAGE(
    digital_marketing_campaign_dataset[ConversionRate]
)
```

### Average Time on Site

```dax
Average Time On Site =
AVERAGE(
    digital_marketing_campaign_dataset[TimeOnSite]
)
```

### Average Loyalty Points

```dax
Average Loyalty Points =
AVERAGE(
    digital_marketing_campaign_dataset[LoyaltyPoints]
)
```

### Average Customer Age

```dax
Average Age =
AVERAGE(
    digital_marketing_campaign_dataset[Age]
)
```

### Customer Record Count

```dax
Customer Count =
COUNT(
    digital_marketing_campaign_dataset[CustomerID]
)
```

The average CTR and conversion measures calculate arithmetic means of row-level rates. They are not weighted overall rates.

## Analysis Workflow

1. Import the CSV dataset through Power Query.
2. Promote the first row to column headers.
3. Assign appropriate data types to the 20 fields.
4. Create a dedicated measure table.
5. Define measures for engagement, demographics, and campaign rates.
6. Compare channels and campaign types using tables and charts.
7. Present the results in a single-page dashboard.

## Business Recommendations

- Investigate Social Media's higher displayed average conversion rate before considering budget changes.
- Review Referral expenditure alongside attributable conversions and revenue.
- Examine whether PPC's higher CTR translates into valuable customer actions.
- Evaluate campaign types using metrics aligned with their objectives.
- Use customer demographics to inform audience testing.
- Add validated cost-per-conversion and revenue metrics before assessing marketing efficiency.

These are proposed analytical actions. Their business impact has not been measured.

## Repository Contents

| File | Description |
|---|---|
| `Digital Marketing analysis project.pbit` | Power BI report template |
| `screenshort 1.jpeg` | Dashboard screenshot |
| `README.md` | Project documentation |

## How to Open the Project

1. Download or clone this repository.
2. Open `Digital Marketing analysis project.pbit` in Power BI Desktop.
3. Open Power Query.
4. Update the CSV file path in the Source step.
5. Connect to a compatible CSV containing the expected fields.
6. Apply changes and refresh the report.

> The template references a CSV file on the author's local computer. The source CSV is not included in the repository.

## Limitations and Future Improvements

- Document the dataset source, reporting period, and record-level definition.
- Include the source CSV where sharing permissions allow.
- Replace the fixed local path with a configurable parameter.
- Validate customer ID uniqueness before reporting unique customers.
- Confirm that advertising spend is additive across records.
- Rename the email measure to reflect its click-to-open denominator.
- Apply consistent percentage formatting.
- Restore visible values and complete labels in the KPI panels.
- Clarify the units used for TimeOnSite.
- Use clearly labelled axes when comparing advertising spend and customer counts.
- Add impressions and clicks for weighted CTR calculations.
- Add attributable revenue and validated conversion counts for efficiency analysis.
- Introduce date fields for campaign trend analysis.

## Author

**Junaed Bogdadi**

[GitHub Profile](https://github.com/junaed-bogdadi)
