---
title: Numbers &amp; Arrows in Dashboards
excerpt: We've been really busy in GoodData in the past couple months reshaping our upload APIs - simplifying them, speeding them up and opening them up to more flexibility. In summer we've released our v2.0 APIs to our developer community through our GoodData CL. Now we're back with the latest installment - SLI API allowing you to load a single file and have it normalized in GoodData. Read more on how to start using them.
layout: post
---
# Numbers &amp; Arrows in Dashboards

Some of you have written in and asked how we achieved our nice [GetSatisfaction health dashboards](http://www.gooddata.com/blog/get-satisfaction-and-gooddata-team-up-to-transform-social-engagement-metrics/) with large numbers and progress indicators. Since this is a bit of a hack, I decided this would be a good audience to explain the trick. We do intend to implement this feature properly - in about a month. However, in the mean time, some clever tricks / a bit of wrestling can get you this effect today:
<img src="http://www.gooddata.com/files/2010/10/GetSatisfaction-Dashboard.jpg" alt="Custom Arrows Formatting">

###Large Font Numeric Report:

1. Create a report showing a single number (remove all attributes in the How section)
2. Convert the report to a stack bar chart
3. In the right column > **Advanced Configuration** > **Y Axis** > **Primary Axis**, set the **max** of the axis to something several orders of magnitude larger then your data - for example 1000000000 (depending on your number), and untick the **Name** and **Labels** checkboxes
4. In Advanced Configuration > Global Settings, make sure **Data Labels** is checked, set the font size to 18, turn off **Values** and **Boxed**, but keep **Totals**
<p><img src="/images/posts/chart-settings.png" alt="Chart Settings"></p>

###Trending Colored Arrows:
5. To show a positive/negative trend, you need to create a second metric showing a difference in time. Here is a MAQL example for a metric called `Revenue`, showing trend between last month and the month before it (attribute `Month`):
<pre><code>SELECT (SELECT Revenues FOR Previous(Month, 1)) - (SELECT Revenues FOR Previous(Month, 2))</code></pre>
You will need to create this as a [Advanced Custom Metric](https://secure.gooddata.com/docs/html/reference.guide.createmetrics.advancedMetricEditor.html#reference.guide.createmetrics.advanced.custom). See more documentation on [floating date metrics](https://secure.gooddata.com/docs/html/reference.guide.maql.previousPeriod.html).
6. Create a customized formatting for this metric. Here's where the trick get's a bit hairy, full documentation is [available here](https://secure.gooddata.com/docs/html/reference.guide.reportoptions.formatting.html). We're using both conditional formatting (different for negative and positive numbers) and changing the font color. For the final trick, we provide a Unicode symbol for up/down arrow. The final formatting string looks like this:
<pre><code>[green]▲;[red]▼</code></pre>
<p><img src="/images/posts/custom-arrows-formatting.png" alt="Custom Arrows Formatting"></p>
You can choose your own symbols/arrows, for example by copy/pasting them from Wikipedia ([shapes](http://en.wikipedia.org/wiki/Geometric_shapes), [arrows](http://en.wikipedia.org/wiki/Arrow_%28symbol%29)).