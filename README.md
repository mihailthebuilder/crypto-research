# Crypto Investing Research

A collection of research pieces I've done on crypto investing.

- [Crypto Investing Research](#crypto-investing-research)
  - [Can Bitcoin add value to a portfolio of diversified traditional assets?](#can-bitcoin-add-value-to-a-portfolio-of-diversified-traditional-assets)
    - [Synopsis](#synopsis)
    - [Data sourcing](#data-sourcing)
    - [Asset correlations](#asset-correlations)
    - [Correlation changes over time](#correlation-changes-over-time)
    - [Replicating the research](#replicating-the-research)
  - [Other topics to cover](#other-topics-to-cover)

## Can Bitcoin add value to a portfolio of diversified traditional assets?

### Synopsis

One of the most common reasons why people decide to buy Bitcoin is because they believe it offers diversification benefits for a portfolio of traditional assets. [Empirical research](https://research.ark-invest.com/hubfs/1_Download_Files_ARK-Invest/White_Papers/ARKinvest_091729_Whitepaper_Bitcoin_II_An%20Investment.pdf?hsCtaTracking=71be7529-9a39-404e-97b3-04fd4ccf80ec%7C07365ce1-0ed3-4835-9c3c-ac33c030cd70) from Cathie Wood's ARK invest seems to prove this:

![ark correlation](ark_corr.png)

However, there's a ton of misinformation about cryptos these days so I wanted to personally verify the theory.

### Data sourcing

I fetched daily close prices from 16 Aug 2010 to 15 Sep 2021 for Bitcoin and the following three ETF index trackers:

- Vanguard Total World Stock ETF (VT) - covers all equity markets globally (developed & emerging)
- Vanguard Total Bond Market ETF (BND) - provides exposure to the investment-grade, US dollar-denominated bond market
- iShares International Treasury Bond ETF (IGOV) - offers exposure to non-US dollar denominated investment-grade bonds

I picked ETFs instead of indices (e.g. S&P 500) because the results are more practical. No one cares about hypothetical returns for an index; they want to know what portfolio construction choices they should make based on securities they can actually purchase.

VT is, in my view, the best proxy for a globally-diversified portfolio of equities. Combining BND and IGOV (weighed equally) represents the best compromise for an equivalent in the bonds market. Vanguard's BNDX is actually a more suitable complement to BND, but its inception date is 4 Jun 2013, which would've meant losing two years of data.

I placed all the historical price data in a single pandas DataFrame, then calculated the rolling 12-month logarithmic returns.

### Asset correlations

I used pandas' `corr` method to get the correlation matrix between the returns for Bitcoin and the Equities (VT) and Bonds (BND x 50% + IGOV x 50%) portfolios. I then created a heatmap with the matrix:

![correlation matrix](btc-corr.png)

The results show a somewhat higher correlation between Bitcoin and equities compared to the ARK paper (0.44 vs 0.26). But it's still sufficiently small to allow for potential diversification benefits. The Bitcoin/bonds correlation paints a similar story (0.11 vs -0.14).

### Correlation changes over time

Bitcoin has shot up in popularity since it started trading in 2010. Because of that, I was worried that the above correlation figures might be hiding a trend of significant rises over the last few years, when the cryptocurrency has effectively become mainstream.

![correlation matrix timeseries](btc-corr-ts.png)

### Replicating the research

See the [btc.ipynb](./btc.ipynb) Jupyter notebook.

## Other topics to cover

- [ ] how BTC correlation changes over time
- [ ] BTC + funds
- [ ] index development
