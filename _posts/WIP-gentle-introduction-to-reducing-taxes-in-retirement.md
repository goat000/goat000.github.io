---
layout: 
title: A gentle introduction to reducing taxes in retirement
subtitle: "Or: fun with sliders"
# cover-img: /assets/img/path.jpg
# thumbnail-img: /assets/img/thumb.png
# share-img: /assets/img/path.jpg
tags: drawdown, retirement, tax, interactive
# author: Brian Williammee
---
Let's start simple, and then add one concept at a time, until we get somewhere useful for real-life retirement drawdown planning.  We'll start with these assumptions:

* You have $100,000 in savings, all in a traditional IRA
* You plan to withdraw it over the next 3 years, starting in 2024
  - Maybe because you plan on relying on social security after that, but mostly for the sake of having a simple exercise
* You and your spouse are 60 years old, which means:
  - You can draw from retirement accounts with no penalty (you're older than 59.5)
  - You are not receiving Social Security payments yet (you're younger than 62)
  - You are not subject to Required Minimum Distribution (you're younger than 72)
* You file taxes as married filing jointly, and you use the standard deduction. You have no tax credits, and no dependents
* Your investment returns are 0%, inflation is 0%, and federal tax brackets and standard deduction will not change in the next few years.

**How do you minimize the taxes you pay on those three years of withdrawals?**
I encourage you to play around with the sliders below before looking at the answer.



<!--<meta name="viewport" content="width=device-width, initial-scale=1.0">-->
<!-- Most of the IDs and strings in this file are also used in the Selenium tests in integration_tests/test_example1.py -->
<!-- So make sure to update those when messing with these. -->
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
        <input type="text" id="zero-percent-value" class="bucket-value-numeric" readonly/>
        <input type="text" id="zero-percent-tax" class="bucket-value-numeric" style="margin-bottom:25px;" readonly/>
        <div class="bucket-label">Withdrawals taxed at 10%</div>
        <div class="bucket-container">
            <div class="bucket-fill" id="ten-percent-bucket"></div>
        </div>
        <input type="text" id="ten-percent-value" class="bucket-value-numeric" readonly/>
        <input type="text" id="ten-percent-tax" class="bucket-value-numeric" style="margin-bottom:25px;" readonly/>
        <div class="bucket-label">Withdrawals taxed at 12%</div>
        <div class="bucket-container">
            <div class="bucket-fill"  id="twelve-percent-bucket"></div>
        </div>
        <input type="text" id="twelve-percent-value" class="bucket-value-numeric" readonly/>
        <input type="text" id="twelve-percent-tax" class="bucket-value-numeric" style="margin-bottom:25px;" readonly/>
    </div>
    <div class="arrow"><p style="grid-row:2">➡️</p></div>
    <div class="results">
        <div style="grid-row: 2; font-weight:bold">Total tax paid on all withdrawals</div>
        <input type="text" id="total-tax" class="total-tax" style="grid-row: 3; font-weight:bold; font-size: 20px;" readonly/>
        <div style="grid-row: 4;" id="min-tax-or-not"></div>
    </div>
</div>

