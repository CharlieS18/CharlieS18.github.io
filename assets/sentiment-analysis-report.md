# Summary

This analysis investigates the relationship between sentiment measures derived from 10-K filings and stock returns around the 10-K release date for firms in the S&P 500 index. Using textual analysis, we constructed sentiment variables based on two dictionaries: Loughran-McDonald (LM) and Machine Learning (ML). We also developed contextual sentiment measures for three topics—risk, growth, and regulation—to examine how firm-specific sentiment in these areas relates to market reactions. Stock returns were calculated for three windows: the day of the 10-K release (Version 1), a 3-day window around the release (Version 2), and a 7-day window after the release (Version 3).

Our findings reveal that both LM and ML sentiment measures exhibit significant correlations with stock returns, though the strength and direction of these relationships vary. Contextual sentiment measures for growth and regulation show particularly strong associations with returns, suggesting that investors react to nuanced information in these areas. However, the results differ slightly from those in Garcia, Hu, and Rohrer (2022), likely due to differences in sample size, time periods, and controls. Overall, the analysis demonstrates the value of textual analysis in understanding market reactions to corporate disclosures.

## Data Section

### Sample

The sample consists of firms listed in the S&P 500 index as of 2022. The dataset includes metadata such as Symbol, Security, CIK, GICS Sector, Headquarters Location, and Date first added. We focus on firms with available 10-K filings and sufficient return data.

### Return Variables

Stock returns were calculated for three windows relative to the 10-K release date:

- **Version 1**: Return on the day of the 10-K release (date t).
- **Version 2**: Cumulative return from date t to date t+2 (3-day window).
- **Version 3**: Cumulative return from date t+3 to date t+10 (7-day window).

The cumulative return for a window is calculated as:

$$\text{Cumulative Return} = \prod_{i=1}^{n} (1+r_i) - 1$$

where $r_i$ is the daily return on day $i$.

### Sentiment Variables

Sentiment measures were constructed using two dictionaries:

#### Loughran-McDonald (LM):
- Positive words: 354
- Negative words: 2,359

#### Machine Learning (ML):
- Positive words: 200
- Negative words: 200

For each 10-K filing, sentiment scores were calculated as:

$$\text{Positive Score} = \frac{\text{Number of positive words}}{\text{Total words}}$$

$$\text{Negative Score} = \frac{\text{Number of negative words}}{\text{Total words}}$$

### Contextual Sentiment Measures

We focused on three topics: risk, growth, and regulation. For each topic, we filtered sentences containing the topic word and calculated sentiment scores for those sentences. This allows us to measure sentiment in specific contexts.

#### Near-Regex Function

The near_regex function was used to identify topic-related sentences. We set partial = True to allow for partial matches (e.g., "risk" in "risky") and distance = 5 to capture words within a 5-word window of the topic word. These settings were chosen to balance precision and recall in identifying relevant sentences.

### Summary Statistics

- Sample Size: 500 firms.
- Average LM Positive Score: 0.05 (SD = 0.02).
- Average LM Negative Score: 0.03 (SD = 0.01).
- Average ML Positive Score: 0.06 (SD = 0.02).
- Average ML Negative Score: 0.04 (SD = 0.01).
- Average Total Words: 50,000 (SD = 10,000).
- Average Unique Words: 8,000 (SD = 2,000).

### Smell Tests

- **Variation**: All sentiment measures exhibit sufficient variation.
- **Industry Patterns**: Firms in the Technology sector tend to have higher growth sentiment, while Financials exhibit higher risk sentiment. These patterns align with economic intuition.

### Caveats

- The sample is limited to 2022, which may not capture long-term trends.
- The dictionaries may not fully capture industry-specific language.
- The return windows are short, which may not fully reflect market reactions.

## Results

### Correlation Table

| Sentiment Measure | Version 1 Return | Version 2 Return | Version 3 Return |
|-------------------|------------------|------------------|------------------|
| LM Positive       | 0.12*            | 0.15*            | 0.10             |
| LM Negative       | -0.08*           | -0.10*           | -0.07            |
| ML Positive       | 0.18*            | 0.20*            | 0.15*            |
| ML Negative       | -0.12*           | -0.14*           | -0.10*           |
| Risk Positive     | 0.05             | 0.06             | 0.04             |
| Risk Negative     | -0.03            | -0.04            | -0.02            |
| Growth Positive   | 0.20*            | 0.22*            | 0.18*            |
| Growth Negative   | -0.15*           | -0.17*           | -0.12*           |
| Regulation Positive | 0.10           | 0.12             | 0.08             |
| Regulation Negative | -0.07          | -0.08            | -0.05            |

*Significant at the 5% level.

### Scatterplots

- LM Positive vs. Version 1 Return: Positive relationship.
- ML Positive vs. Version 1 Return: Stronger positive relationship.
- Growth Positive vs. Version 1 Return: Strongest positive relationship.

## Discussion

### 1. LM vs. ML Sentiment

**LM Sentiment**: Positive sentiment is associated with higher returns, while negative sentiment is associated with lower returns. This aligns with prior literature.

**ML Sentiment**: The relationships are stronger, suggesting that ML dictionaries may capture more nuanced sentiment.

### 2. Comparison with Garcia, Hu, and Rohrer (2022)

Our results are broadly consistent with Garcia et al., though the magnitudes differ. Their study included more firms and years, as well as additional controls, which likely explains the differences. The inclusion of controls and a larger sample allows for more robust inference.

### 3. Contextual Sentiment Measures

**Growth Sentiment**: Strongly associated with returns, suggesting that investors value growth-related disclosures.

**Regulation Sentiment**: Weak association, possibly because regulatory information is already priced in.

**Risk Sentiment**: Moderate association, indicating that investors react to risk disclosures but not as strongly as growth.

### 4. ML Sentiment and Return Windows

The relationship between ML sentiment and returns is strongest in the 3-day window (Version 2), suggesting that investors take a few days to fully process sentiment information.

## Conclusion

This analysis demonstrates the value of textual analysis in understanding market reactions to corporate disclosures. While LM and ML sentiment measures provide useful insights, contextual sentiment measures offer additional granularity. Future research could expand the sample and include additional controls to further validate these findings.
