---
layout: 
title: A gentle introduction to reducing taxes in retirement
subtitle: "Or: fun with sliders"
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/gentle-introduction-to-reducing-taxes-in-retirement.webp
# share-img: /assets/img/path.jpg
tags: drawdown, retirement, tax, interactive
# author: Brian Williammee
---

I want to do a series of posts that build towards a calculator useful framework for real-life
retirement drawdown planning.  The end result, if I get that far, will be:
* A retirement drawdown calculator that takes in real-life details and provides a tax-optimized and
Obamacare-optimized drawdown plan covering all the expected years of retirement.
* A series of posts that explain all the concepts used in the calculator.

To begin with, let's play a simple game to demonstrate a simple tax planning concept.  We can build
on it in future posts.

## Rules
* **Your goal: Find the lowest possible federal tax amount for the following situation.**
* You have $100,000 in savings, all in a traditional IRA
* You plan to withdraw it over the next 3 years, starting in 2024
* You file taxes as married filing jointly, and you use the standard deduction. You have no tax
credits, and no dependents
* Your investment returns are 0%, inflation is 0%, and federal tax brackets and standard deduction
will not change in the next 3 years.
* You and your spouse are 60 years old, which means:
  - You can draw from retirement accounts with no penalty
  - You are not receiving Social Security payments yet
  - You are not subject to Required Minimum Distribution


I encourage you to play around with the sliders below before looking at the solution below.

## Super-fun game - minimize your tax burden

<div style="font-size: smaller">This exercise currently does not work on mobile devices.  Apologies!</div>
<!-- Most of the IDs and strings in this file are also used in the Selenium tests in integration_tests/test_example1.py -->
<!-- So make sure to update those when updating these. -->
<div id="flexbox-container">
    <div id="sliders">
        <div id="tax-bracket-indicator-container" style="grid-row: 2; grid-column: 1;">
            <div class="tax-bracket-indicator" style="grid-row: 1; grid-column: 1; background-color:#B66">12%</div>
            <div class="tax-bracket-indicator" style="grid-row: 2; grid-column: 1; background-color:#FF6">10%</div>
            <div class="tax-bracket-indicator" style="grid-row: 3; grid-column: 1; background-color:#6B6">0%</div>
        </div>
        <div class="slider-label" style="grid-row: 1; grid-column: 2;">Year 1 Withdrawal</div>
        <div class="slider-container" style="grid-row: 2; grid-column: 2;">
            <div id="slider-vertical-0" class="slider-vertical">
                <div id="slider-filled-0" class="slider-filled"></div>
            </div>
        </div>
        <input type="text" id="slider-value-0" class="slider-value-input" style="grid-row: 3; grid-column: 2;"/>
        <div class="slider-label" style="grid-row: 1; grid-column: 3">Year 2 Withdrawal</div>
        <div class="slider-container" style="grid-row: 2; grid-column: 3;">                
            <div id="slider-vertical-1" class="slider-vertical">
                <div id="slider-filled-1" class="slider-filled"></div>
            </div>
        </div>
        <input type="text" id="slider-value-1" class="slider-value-input" style="grid-row: 3; grid-column: 3;"/>
        <div class="slider-label" style="grid-row: 1; grid-column: 4">Year 3 Withdrawal</div>
        <div class="slider-container" style="grid-row: 2; grid-column: 4;">
            <div id="slider-vertical-2" class="slider-vertical">
                <div id="slider-filled-2" class="slider-filled"></div>
            </div>                
        </div>
        <input type="text" id="slider-value-2" class="slider-value-input" style="grid-row: 3; grid-column: 4;"/>
        <div id="full-withdrawal-or-not" style="grid-row: 4; grid-column-start: 1; grid-column-end: 5;"></div>
    </div>
    <div class="arrow"><p style="grid-row:2">➡️</p></div>
    <div class="buckets">
        <div class="bucket-label">Withdrawals taxed at 0%</div>
        <div class="bucket-container">
            <div class="bucket-fill" id="zero-percent-bucket"></div>
        </div>
        <div id="zero-percent-value" class="bucket-value-numeric"></div>
        <div id="zero-percent-tax" class="bucket-value-numeric" style="margin-bottom:25px;"></div>
        <div class="bucket-label">Withdrawals taxed at 10%</div>
        <div class="bucket-container">
            <div class="bucket-fill" id="ten-percent-bucket"></div>
        </div>
        <div id="ten-percent-value" class="bucket-value-numeric"></div>
        <div id="ten-percent-tax" class="bucket-value-numeric" style="margin-bottom:25px;"></div>
        <div class="bucket-label">Withdrawals taxed at 12%</div>
        <div class="bucket-container">
            <div class="bucket-fill"  id="twelve-percent-bucket"></div>
        </div>
        <div id="twelve-percent-value" class="bucket-value-numeric"></div>
        <div id="twelve-percent-tax" class="bucket-value-numeric" style="margin-bottom:25px;"></div>
    </div>
    <div class="arrow"><p style="grid-row:2">➡️</p></div>
    <div class="results">
        <div style="grid-row: 2; font-weight:bold">Total tax paid on all withdrawals</div>
        <div id="total-tax" class="total-tax" style="grid-row: 3; font-weight:bold; font-size: 20px;"></div>
        <div style="grid-row: 4;" id="min-tax-or-not"></div>
    </div>
</div>

As long as you withdraw at least $29200 each year, you'll pay $1240 in federal income taxes overall.
If you withdraw less than that in any one year, you won't "use up" the full amount of your standard
deduction that year, and that will show up as higher taxes in one of the other years, leading to
higher taxes overall.

The worst outcome is to withdraw all of the money in one year.  If you do that, you'll pay $8032!
That's more than *six times* as much as if you withdraw evenly!

That'll all because of the progressive nature of federal income tax.  As you add more income in a
single year, you increase not just the amount subject to taxation, but the *tax rate* itself.  The
relevant income tax rates for the game in this post are:

| Rate | Income, for Married Filing Jointly (in 2024) |
| ----------------------------------- | ------------- |
|  0% (because of standard deduction) | First $29,200 |
| 10%                                 | Next  $11,600 |
| 12%                                 | Next  $35,500 |

The numbers are different for different tax statuses (Single, Married Filing Separately, Head of
Household), but the same concept applies.

## Conclusion
* **Fill the lowest-tax buckets first.**  You will generally want to plan out retirement to make the
maximum possible 0%-taxed withdrawals every year, before planning on any withdrawals in the 10%
bracket.  The same is true for taking the maximum possible 10%-taxed withdrawals every year before
planning on any withdrawals in the 12% bracket, and so on.  You can also think of it as *spreading
out your retirement income evenly* over the years.
