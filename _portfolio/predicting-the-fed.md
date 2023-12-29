---
title: "Interest Rate Analysis"
seo_title: "Interest Rate Analysis"
excerpt: "a deep dive into NBA referee impact on gameplay"
image: "/images/12.jpg"
author_profile: false
collection: portfolio
---
{% include base_path %}
{% seo %}
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&display=swap');

/* Ensure the body has no margin, which could prevent the image from touching the left side */
body, html {
  margin: 0;
  padding: 0;
  overflow-x: hidden; /* Prevent horizontal scroll */
}

.full-screen-background {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw; /* Full viewport width */
  height: 70vh; /* Adjusted height */
  background-image: url('/images/FedReserve.webp'); 
  background-size: cover;
  background-position: center center;
  position: absolute; /* or 'fixed' if you want it to stay in place on scroll */
    left: 0; /* Align to the very left of the viewport */
    top: 11vh; /* Align to the very top of the viewport */
    right: 0; /* Ensure it stretches to the very right of the viewport */
    margin: 0; /* Override any inherited margins */
}

.overlay-text {
  text-align: center;
  font-family: 'Inter', sans-serif;
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 10px;
  padding: 1em; /* Adjusted padding */
  box-sizing: border-box;
  color: white;
  width: 80%;
  max-width: 750px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Adjust the margins between lines as needed */
.overlay-text h1 {
  font-size: 3em;
  font-weight: 700;
  margin: 0 0 0.1em 0; /* Increased space after the title */
}

.overlay-text h2 {
  font-size: 1.15em;
  font-weight: 400;
  margin: 0 0 0.5em 0; /* Increased space after the subtitle */
}

.overlay-text h3 {
  font-size: 0.90em;
  font-weight: 700;
  margin: 0 0 0.25em 0; /* Smaller space after the byline */
}

.overlay-text p {
  font-size: 0.75em;
  font-weight: 300;
  margin: 0; /* No additional space after the date */
}

.content {
  padding-top: 150vh; /* Increase this value to push content down further */
  padding-left: 20px;
  padding-right: 20px;
  padding-bottom: 20px;
}

@media screen and (max-width: 768px) {
  .spacer {
    height: 70vh; /* Adjust for smaller screens */
  }
}

.spacer {
  height: 60vh; /* Adjust this value as needed */
}

</style>

<div class="full-screen-background">
  <div class="overlay-text">
    <h1>Predicting the Fed</h1>
    <h2>Which platform offers the most accurate forecast of the federal funds rate?</h2>
    <h3>By: Blake Law</h3>
    <p>Dec 27, 2023</p>
  </div>
</div>


<div class="spacer"></div>

## Introduction


Interest rates impact the entire economy. A high mortgage rate might discourage potential homebuyers. A low interest rate on loans improves access to credit for startups looking to scale. More broadly, the interest rate has profound impacts on two fundamental indicators: the unemployment rate and inflation.

The *Federal Open Market Committee (FOMC)*, a branch of the Federal Reserve, meets eight times a year to set a target range for the federal funds rate, the interest rate banks charge each other for reserve balances that aren’t backed by collateral. While this sounds like an esoteric situation to target, it has ripple effects on every other interest rate, although at varying levels. Most directly, it affects short-term interest rates, such as Treasury bills or the prime rate, the interest banks charge on customers with good credit. However, it can also affect longer term interest rates such as 30 year bonds and mortgages.


<p align="center" style="padding-top: 10px;">
    <img src="/images/FFR.png" alt="example image" width="500" style="margin-bottom: 5px;">
    <br>
    <em>Federal funds rate compared to other securities</em>
</p>


The exact range the FOMC, composed of twelve members, sets depends on what the committee views will meet the Fed’s Dual Mandate, which aims to achieve maximum employment and price stability. In the last three meetings, held in September, November, and December of this year, the committee chose to keep the target rate unchanged at $$5.25-5.50\%$$, the highest rate in 22 years.

<p align="center" style="padding-top: 10px;">
    <img src="/images/Lower.png" alt="example image" width="500" style="margin-bottom: 5px;">
    <br>
    <em>Lower limit of the federal funds rate, 2019 – Present</em>
</p>



How can we predict what the FOMC will set before it actually announces its decision? Knowing ahead of time what the interest rate will be has enormous importance: it can influence investment decisions, the stock market, and consumer behavior. Besides looking at the [size of a briefcase](https://www.stlouisfed.org/publications/regional-economist/july-2000/inside-the-briefcase-the-art-of-predicting-the-federal-reserve), there are some tools available to us. The most popular is the [**CME FedWatch**](https://www.cmegroup.com/markets/interest-rates/cme-fedwatch-tool.html), which provides probabilities for each target range. Another relatively new method is utilizing online prediction markets, such as [**Kalshi**](https://kalshi.com/), founded in 2018. But which one is more accurate?

### How FedWatch Works

The CME Fedwatch Tool, launched in 2013 by the CME Group, a financial services company which largely deals in the derivatives market, provides probabilities daily for each upcoming meeting and their potential target ranges. For instance, at the time of writing this article, there is a roughly $$81.4\%$$ chance that in the January 2024 meeting the Fed will keep interest rates unchanged, and a $$18.6\%$$ chance that they will cut rates by 25 bps (basis points) to $$5.00-5.25\%$$.


<p align="center" style="padding-top: 10px;">
    <img src="/images/CME.png" alt="example image" width="500" style="margin-bottom: 5px;">
    <br>
    <em>Probability history for the upcoming Jan. 2024 meeting</em>
</p>




The probabilities for each range are [based on Fed Fund futures](https://www.cmegroup.com/articles/2023/understanding-the-cme-group-fedwatch-tool-methodology.html), which are traded on the Chicago Mercantile Exchange (CME). For instance, take a look at [ZQF24](https://frickservices.com/markets/chart.php?symbol=ZQF24&density=X&period=W), the 30-day federal funds futures for the January 2024 meeting. To find the estimated [effective federal funds rate](https://www.newyorkfed.org/markets/reference-rates/effr) at a given time, take $$100 - Price$$. The current price (as of Dec 27, 2023) is $$94.67$$, implying an effective rate of $$5.33\%$$, on the lower end of the $$5.25-5.50\%$$ range.

The data is not available in real time: quotes are currently delayed by “at least 10 minutes” and beginning in April of next year, [“settlement data … will have a delayed publication time of 12:00 a.m. CT”](https://www.cmegroup.com/markets/interest-rates/stirs/30-day-federal-fund.quotes.html#venue=globex). Want real-time access? That will be [$24,000 a year for a distribution license](https://www.cmegroup.com/market-data/distributor/files/mdla-cme-schedule-5-apr-2020.pdf) and monthly device fees on top of that.

These futures inform the probabilities that the FedWatch publishes daily, with the regular assumptions such as rate changes being in increments of 25 bps and the effective rate being bounded by zero (this is not so true in [other countries](https://apnews.com/article/japan-economy-rates-interest-boj-e2deca211671f14f1f3d6277ed3ad3bb)).

### How Kalshi Works

Kalshi is a financial exchange that offers event contracts. Founded by MIT alumni Tarek Mansour and Luana Lopes Lara, it became the [“first federally regulated event-based trading exchange in U.S. history”](https://www.forbes.com/sites/alexandrawilson1/2021/12/01/by-the-numbers-meet-the-forbes-30-under-30-class-of-2022/?sh=172d70c4663b) after receiving a federal license from the Commodities Futures Trading Commission (CFTC) in 2021. Personally, I started using the site a few months after it launched, being a fan of [PredictIt](https://www.predictit.org/) previously, but discouraged by the lack of non-political markets. Kalshi, on the other hand, provides a wider array of markets (I’ve traded whether it would rain in Seattle), but does not currently offer [political markets](https://www.reuters.com/world/us/predictions-market-kalshi-sues-cftc-blocking-election-contracts-2023-11-01/), which they are currently litigating.

Event contracts are binary: either the market resolves ‘yes’ or ‘no’, with a $1 denomination per contract. The prices for the market are completely based on the participants of the site, which are [majority retail traders](https://kalshi.com/blog/article/who-am-i-trading-against-on-kalshi?). Technically, when people trade, they aren’t directly trading with each other, but with a regulated clearing house, which has a legal obligation to complete the trade as a counterparty, and is fully collateralized. Kalshi makes money with [trading fees](https://kalshi.com/docs/kalshi-fee-schedule.pdf).


<p align="center" style="padding-top: 10px;">
    <img src="/images/KalshiRain.png" alt="example image" width="500" style="margin-bottom: 5px;">
    <br>
    <em>Sample market on kalshi.com</em>
</p>



The federal funds market in question is found [here](https://kalshi.com/markets/fed/fed-funds-rate#fed-24jan). While FedWatch produces probabilities based on ranges, Kalshi operates on a 'above $$X\%$$' basis; for example, the 'above $$5.25\%$$' contract is currently trading at $$98$$ cents, indicating a roughly $$98\%$$ probability that the target rate will exceed that value following the January 2024 meeting

## Data Collection

To compare the two markets, I extracted the historical prices for three meetings over time: December, November, and September 2023. For Kalshi, I wrote a script in Python using their [API](https://github.com/Kalshi/kalshi-python). To transform the data for comparison, I used differences between contracts to infer the probability of a target range. For instance, if there is a $$90\%$$ that the rate is above $$5.25\%$$, and $$50\%$$ chance the rate is above $$5.50\%$$, we can infer a $$40\%$$ chance that the rate will be set at $$5.25-5.50\%$$.

The CME FedWatch provides CSV downloads for their historical data. Unfortunately, it only goes back to September of this year. While they do have an API, it is [paid](https://www.cmegroup.com/market-data/market-data-api.html) and requires contacting their team with a business email and phone number.

## Analysis

To directly compare Kalshi and FedWatch, I found the *implied interest rate* by weighting each target range with the probability provided at a given time. For instance, in the FedWatch example earlier, the **implied rate** (which we will denote IR) for January 2024 based on today’s expectations is calculated as

$$IR = 512.5 \cdot 0.186 + 537.5 \cdot 0.814 = 532.85 \text{ bps } (5.33\%)$$


In this calculation, we took the probability (the second number) and multiplied it by the midpoint of the range in basis points (the first number). This is essentially an expected value. For the FedWatch, I was able to calculate implied target rates daily, and for Kalshi as often as people trade, which is [8AM-12AM](https://help.kalshi.com/faq/what-are-trading-hours) five days a week and 8AM-10PM two days.

Let’s take a look at the results:

<div class="slideshow-container text-center">
    <!-- Full-width images within slides with captions -->
    <div class="mySlides">
        <img src="/images/Sep23.png" style="width:100%">
        <div class="caption">September 20th, 2023 Meeting</div>
    </div>
    <div class="mySlides">
        <img src="/images/Nov23.png" style="width:100%">
        <div class="caption">November 1st, 2023 Meeting</div>
    </div>
    <div class="mySlides">
        <img src="/images/Dec23.png" style="width:100%">
        <div class="caption">December 13th, 2023 Meeting</div>
    </div>

    <!-- Arrows -->
    <a class="prev" onclick="changeSlide(-1)">&#10094;</a>
    <a class="next" onclick="changeSlide(1)">&#10095;</a>
</div>

<style>
.slideshow-container {
  position: relative;
  max-width: 65%;
  margin: auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.caption {
  color: #333; /* Slightly lighter black font */
  font-size: 16px; /* Regular font size */
  text-align: center;
  width: 100%; /* Full width to match the image */
  position: relative; /* Relative to the slideshow container */
  margin-top: 8px; /* Space above the caption */
  font-family: Arial, sans-serif; /* Standard font */
}


.mySlides {
  display: none;
}

.mySlides:first-child {
  display: block;
}

img {
  vertical-align: middle;
  border-radius: 8px;
}

/* Arrows style */
.prev, .next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  color: #333;
  font-size: 24px;
  padding: 16px;
  user-select: none;
  z-index: 100;
  background: transparent;
  border: none;
}

/* Positioning the arrows completely outside of the image */
.prev {
  left: calc(0% - 40px); /* Adjust left position here */
}

.next {
  right: calc(0% - 40px); /* Adjust right position here */
}
</style>

<script>
var slideIndex = 0;
showSlides(slideIndex);

function showSlides(n) {
    var i;
    var slides = document.getElementsByClassName("mySlides");
    if (n >= slides.length) { slideIndex = 0 }
    if (n < 0) { slideIndex = slides.length - 1 }
    for (i = 0; i < slides.length; i++) {
        slides[i].style.display = "none";
    }
    slides[slideIndex].style.display = "block";
}

function changeSlide(n) {
    showSlides(slideIndex += n);
}

// Ensure the first image is displayed when the page loads
window.onload = function() {
    showSlides(slideIndex);
};
</script>
<br>
First, we can visually see something in common with all three charts: Kalshi and FedWatch were roughly in line for most of the year, except for a rather large divergence starting in mid March and continuing until near the end of May, when the FedWatch tool’s expectations dropped sharply, possibly due to signs the economy was cooling down, such as lower inflation.

Second, we can see that both markets were very confident that the target range for the September meeting would be $$5.25-5.50\%$$ since June, while in November and December the markets were on the fence between a rate hike and no change up until around two months before the respective meetings, where they converged to the midpoint, $$5.375\%$$.

Finally, we see slightly more noise in Kalshi’s data, due to lower trading volume and liquidity. This is clearest in the November meeting chart, where there are seemingly random, large fluctuations in January that aren’t explained by economic trends. However, the volume significantly picks up later in the year and becomes nearly as reliable as the FedWatch.

### Measuring accuracy

How can we quantitatively measure which one is more accurate? Rather than use mean-squared error or some standard metric, I decided that the circumstances warrant a special metric, as the target is a range, not a point. So, for a given data point, the error will be scored as follows:

- If the point is within the final range, there is no error.
- If the point is outside the range, take the minimum distance to the boundary closest to it. For instance, $$5.75$$ would correspond to an error of $$0.25$$, while $$5.15$$ would correspond to an error of $$0.10$$.

Mathematically, this can be written as

$$
\text{E}(x) = 
\begin{cases} 
0 & \text{if } A \leq x \leq B \\
|x - A| & \text{if } x < A \\
|x - B| & \text{if } x > B
\end{cases}
$$

With theoretical federal funds target rate being from $A$ to $B$.


<p align="center" style="padding-top: 10px;">
    <img src="/images/metric.png" alt="example image" width="200" style="margin-bottom: 5px;">
    <br>
    <em>Sample error calculations</em>
</p>



With that in mind, let's calculate the average error for each meeting and market. Since prices may add up to over $1.00 on markets, we will divide by the sum of market prices, which themselves are derived by taking the midpoint of the 'yes bid' and 'yes ask' from the order book:

$$\begin{equation}E_{avg} = \frac{1}{N} \cdot \sum_{i=1}^{N}  E\left(\frac{\sum_{j=1}^{K} M_{j} \cdot P_{i,j}}{\sum_{j=1}^{K} P_{i,j}}\right)\end{equation}$$

where

- $$E(x)$$ is the error function
- $$M_{j}$$ is the midpoint of a given federal funds range $j$ 
- $$P_{i,j}$$ is the market price, equal to $$\frac{a_{i,j}+b_{i,j}}{2}$$
- $$a_{i,j}$$ is the yes ask price at time $i$ in range $j$
- $$b_{i,j}$$ is the yes bid price at time $i$ in range $j$
- $$N$$ is the total number of discrete times
- $$K$$ is the total number of target ranges (for instance, in Dec. 2023 $$K = 15$$)

Running this through each of the dataframes yields the following results:





<iframe title="Comparison of Kalshi and CME" aria-label="Table" id="datawrapper-chart-1ryej" src="https://datawrapper.dwcdn.net/1ryej/2/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="255" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r=0;r<e.length;r++)if(e[r].contentWindow===a.source){var i=a.data["datawrapper-height"][t]+"px";e[r].style.height=i}}}))}();
</script>

<br>
**In each of the three meetings, Kalshi is more accurate than FedWatch**, including an impressive $$0.098\%$$ average error for the September meeting, more than half of FedWatch's.

## Conclusion

Kalshi offers a more accurate picture of the federal funds rate over the three FOMC meetings analyzed, offering a $$0.13\%$$ more accurate measure on average. In the future, I would like to look at more meetings to see if this pattern holds. Additional prediction markets, such as [Polymarket](https://polymarket.com/event/will-the-fed-cut-rates-in-2023?tid=1703725210996), could be incorporated into the analysis to strengthen the assessment of whether retail prediction markets outperform the CME. These diverging results also beg the question: with an efficient market, why aren't institutional investors mimicking the trades of Kalshi if they are more accurate, or vice versa?
