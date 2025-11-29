This project demonstrates the possible relationship between levels of interpersonal trust, and trust people have in political instituations such as the UN, legal system, and Political Parties. It is underpinned by a dataset selected from the European Social Survey's data portal. Specifically, the data is obtained from Wave 9 (ESS 9), edition 3.2. Seven trust-related variables were selected from the dataset overall. These variables were ppltrst, trstprl, trstlgl, trstplc, trstplt, trstprt, and trstun. This dataset, combined with the visulisation and interpretation that follows, is used with the intention of answering the research question: are people who lack interpersonal trust also more likely to be distrusting of political / societal instituations? Data preparation, summarisation and visualisation were implemented through a Google Colab notebook which aims to follow standard academic and industry practices.

The Dataset

As afforementioned, the data was sourced from the European Social Survey (ESS), Wave 9. The file name is data.csv, and can be found in this repository. The following variables were selected using ESS' datafile builder:

ppltrst - Most people can be trusted or you can't be too careful: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=ec98db00-4dc3-4d2b-9cec-2ba5a0ea754c
trstprl - Trust in country's parliament: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=64c6cb47-1b9f-46fd-a5d1-7e361b882325
trstlgl - Trust in the legal system: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=9b7d1b0c-6f21-4386-b341-643929ed0b35
trstplc - Trust in the police: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=75644eb7-7153-4e4f-b8a8-647c1093545f
trstplt - Trust in politicians: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=ec8af066-3639-43eb-9268-d04966d5ac16
trstprt - Trust in political parties: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=7bca8e97-9df2-4c0f-a51a-b1c9e76069ec
trstun - Trust in the United Nations: https://ess.sikt.no/en/datafile/b2b0bf39-176b-4eca-8d26-3c05ea83d2cb?tab=1&elems=30bfbbb6-5c32-4311-a2cd-db07bcb90a6a
(DOI: https://doi.org/10.21338/ess9e03_2)

Each of these variables follows the standard ESS 0-10 scale where 0 is equal to no trust, and 10 indicates full trust. Therefore, any value that falls outside of this scale, i.e. is not equal to an number from 0-10, is representative of an invalid response or particiapnt refusal. These values have been treated as missing (NaN - not a number). ESS was selected due to its methodological integrity, extensive documentation, cross-national comparability, and long-established reputation as a high-quality data source for social scientific research. ESS' sample includes just under 50,000 participants, providing substantial statistical power and supporting the reliability of its estimates. Round 9 was chosen because it provides recent, fully processed data with participation from a wide set of European countries (29), while avoiding the incomplete or provisional characteristics that can accompany newer rounds still undergoing post-fieldwork corrections. The Quality Report for overall fieldwork and data quality regarding Wave 9 can be found at https://stessrelpubprodwe.blob.core.windows.net/data/round9/survey/ESS9_quality_report_e02_1.pdf.

Methodology: Data Cleaning, Descriptive Statistics, Data Visualisation

Data Cleaning

Cleaning the data for use in answering the research question focused on ensuring the values outputted in the trust variables fell within the standard ESS scale of 0-10. Before cleaning, there were thousands of missing values. Below is the output when requesting a printed summary of the missing values (only the output for the trust variables has been included):

ppltrst 145
trstprl 1144
trstlgl 1008
trstplc 369
trstplt 913
trstprt 1062
trstun 4390
This output is unsurprising, considering participants consistently (year-on-year) refuse to pass comment related to the United Nations (trstun), which is why we see 4390 missing values for this variable. Participants are more willing to answer questions of interpersonal trust (ppltrst), with only 145 missing values. To clean the data, the numpy library was used to convert any value that did not fall between 0 and 10 inclusive, to NaN - not a number (np.nan). Ensuring all values were acceptable was followed by developing a mean of the institutional trust variables. This was done by taking a mean of each of the scores from trstprl, trstlgl, trstplc, trstplt, trstprt, and trstun. The result of this summary is held in 'trust_variables_mean'. Data cleaning was succeeded by two new variables to develop descriptive statistics and visualisations from: interpersonal trust (based on ppltrst) and institutional trust (based on trust_variables_mean).

Descriptive Statistics

Descriptive statistics were calculated to summarise the key features of the two primary variables in this analysis: interpersonal trust (ppltrst) and institutional trust (trust_variables_mean). These statistics provide a numerical picture of the data and allow us to understand typical levels of trust, the spread of responses, and the distribution across the 0–10 scale. For interpersonal trust (ppltrst), the average trust level is approximately 5.06, with a standard deviation of 2.50, indicating moderate variation among respondents. The middle 50% of responses fall between 3 and 7 (25th–75th percentile), and responses span the full range from 0 to 10, showing that while some respondents report very low trust, others report very high trust. For institutional trust (trust_variables_mean), the average is slightly lower than interpersonal trust at 4.79, with a standard deviation of 2.12, which indicates somewhat less variation than interpersonal trust. The middle 50% of institutional trust scores ranges from 3.33 to 6.33, also spanning the full 0–10 scale. These descriptive statistics provide a foundation for further analysis and visualisations, and help to contextualise the patterns observed in the subsequent visualisations. They confirm that, on average, respondents report slightly higher trust in other people than in institutions, and that responses are distributed broadly. Descriptive statistics alone do not fully answer whether people who lack interpersonal trust are more likely to distrust institutions; they simply highlight the overall levels and spread of trust. Subsequent visualisations, including scatter plots and correlation calculations, are necessary to examine the direct relationship between the two variables.

Data Visualisation

Visualisation techniques were used to explore the distributions of key variables and to examine the relationship between interpersonal trust and institutional trust in a clear and accessible manner. Visualisations complement descriptive statistics by allowing patterns, relationships, and variation in the data to be identified more intuitively than through numerical summaries alone. Two primary forms of visualisation were employed: histograms and a scatter plot with a regression line. All visualisations were produced using Python within a Google Colab notebook, primarily through the Seaborn and Matplotlib libraries.

Histograms:

Histograms were created for both interpersonal trust (ppltrst) and institutional trust (trust_variables_mean). These were used to visualise the distribution of responses across the 0–10 trust scale for each variable. The purpose of these histograms was to assess how trust is generally distributed within the sample, identify where responses tend to cluster, and observe the overall spread and shape of the data (e.g. whether it is symmetrical or skewed). A vertical dashed line indicating the mean was added to each histogram to visually represent the central tendency in relation to the full distribution. This allows for a direct comparison between average trust levels and the frequency of responses across the scale. These plots are particularly useful for contextualising the descriptive statistics and for identifying whether low, moderate, or high trust dominates across respondents.

Scatter Plot and Correlation:

To examine the relationship between interpersonal trust and institutional trust, a scatter plot was created with interpersonal trust (ppltrst) on the x-axis and instituational trust (trust_variables_mean) on the y-axis. Each point in the plot represents an individual respondent, allowing the association between the two variables to be visually assessed. A linear regression line was overlaid onto the scatter plot to summarise the overall direction of the relationship. This enables a clear visual assessment of whether higher levels of interpersonal trust tend to coincide with higher levels of institutional trust. To complement the visual interpretation, a Pearson correlation coefficient was also calculated, providing a numerical measure of the strength and direction of the observed relationship. Together, the scatter plot and correlation coefficient allow the research question, whether individuals who lack interpersonal trust are also more likely to distrust institutions, to be examined both visually and quantitatively.

Key Findings

Analysis of the European Social Survey Wave 9 trust variables reveals clear but nuanced patterns in interpersonal and institutional trust. Descriptive statistics and histograms show that average interpersonal trust (mean = 5.06) is slightly higher than average institutional trust (mean = 4.79), with both variables spanning the full 0–10 scale and exhibiting substantial variation among respondents. This indicates that Europeans, on average, display moderate trust in both people and institutions, though individual attitudes vary widely.

The relationship between interpersonal trust and institutional trust is visualised using a scatter plot with a fitted regression line. The upward trend of the line indicates a positive association between the two variables. This relationship is confirmed numerically by a Pearson correlation coefficient of 0.42, indicating a moderate positive correlation.

Substantively, this suggests that individuals who report lower levels of trust in other people are, on average, more likely to report low levels of trust in political and societal institutions. However, the moderate size of the correlation and the broad vertical dispersion of data points demonstrate that interpersonal trust does not fully determine institutional trust. Many individuals with low interpersonal trust still report moderate or high institutional trust, and vice versa.

Overall, the findings support the existence of a meaningful but non-deterministic relationship between interpersonal and institutional trust, indicating that generalised social trust is an important, but not exclusive, factor in shaping trust in political and societal institutions.

Conclusion

This project set out to examine whether individuals who exhibit low levels of interpersonal trust are also more likely to distrust political and societal institutions. Using trust variables from Wave 9 of the European Social Survey, the analysis combined data cleaning, descriptive statistics, and data visualisation to explore both the distribution of trust and the relationship between its interpersonal and institutional dimensions.

Descriptive statistics showed that, on average, respondents reported moderate levels of both interpersonal trust (ppltrst, mean = 5.06) and institutional trust (trust_variables_mean, mean = 4.79), with institutional trust slightly lower overall. The wide spread of values across the full 0–10 scale for both variables indicates substantial variation in trust across the population. The histograms further demonstrated that while both forms of trust cluster around mid-range values, institutional trust is marginally more skewed towards lower scores.

The relationship between the two forms of trust was examined using a scatter plot and Pearson correlation analysis. The scatter plot revealed a clear upward trend, indicating that higher interpersonal trust is generally associated with higher institutional trust. This was confirmed by a Pearson correlation coefficient of r = 0.42, representing a moderate positive relationship. This suggests that individuals who are more distrustful of other people are, on average, more likely to be distrustful of political and societal institutions.

However, the correlation is not strong enough to imply determinism. There remains considerable variation in institutional trust among individuals with similar levels of interpersonal trust, indicating that additional factors, such as political context, personal experience, and national institutions, also play an important role. Overall, the findings support the conclusion that interpersonal and institutional trust are meaningfully linked, but not interchangeable.
