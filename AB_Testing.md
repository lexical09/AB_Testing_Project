
# A/B Testing 

## Project overview
This project, which is organized base on [this template](https://docs.google.com/document/d/16OX2KDSHI9mSCriyGIATpRGscIW2JmByMd0ITqKYvNg/edit) and evaluated using [this rubric](https://docs.google.com/document/u/1/d/1Hga00A4258wSJ9dir0Td_ZPLeAtJ079UGbM3C0ykUtE/pub?embedded=true), will provide a fully defined design, analyze the results, and propose a high-level follow-on experiment from an actual experiment that was run by Udacity. [The project instructions](https://docs.google.com/document/u/1/d/1aCquhIqsUApgsxQ8-SQBAigFDcfWVVohLEXcV6jWbdI/pub?embedded=True) contain more details.<br>
<br>
> #### Experiment Overview: Free Trial Screener
>At the time of this experiment, Udacity courses currently have two options on the course overview page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.
>
>In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead. This screenshot shows what the experiment looks like.
>
>The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.
>
>The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.
<br>

## Experiment Design
### All Metrics
* **Number of cookies:** Number of unique cookies to view course overview page.
* **Number of clicks:** Number of unique cookies to click the "Start Free Trial" button (which happens before the free trial screener is triggered).
* **Number of user-ids:** Number of users who enroll in the free trial.
* **Click-through-probability:** Number of unique cookies to click the "Start Free Trial" button divided by number of unique cookies to view the course overview page.
* **Gross conversion:** Number of user-ids to complete checkout and enroll in free trial divided by number of unique cookies to click "Start Free Trial" button.
* **Retention:** Number of user-ids to remain enrolled past the 14-day boundary (and thus make atleast one payment) divided by number of users to enroll in the free trial.
* **Net conversion:** Number of user-ids to remain enrolled past the 14-day boundary divided by the number of unique cookies to click the "Start Free Trial" button.

### Metric Choice
**Invariant metrics:**
* **Number of cookies:** This is the unit of diversion for the A/B test. Since the visit to the course overview page occurs before the experiment, this metric is independent of the experiment and thus should be evenly distributed between the control and experiment group.

* **Number of clicks:** Since the users click before the free trial screener pops up, this metric is also independent of the experiment, and should be evenly distributed between the control and experiment groups.

* **Click-through-probability:** This is simply a ratio of the above two metrics, and since they are both independent, this too is independent, and should be evenly distributed between the control and experiment groups.

**Evaluation metrics:**
* **Gross conversion:** The number of user-ids that enroll in the free trial divided by the number of unique cookies to click on the "start free trial" button. The number of enrollments can be affected by the experiment and as a result the gross conversion; therefore this will be used as an evaluation metric. There should be a statisticial significant reduction in enrollment.

* **Retention:** The number of user-ids that stayed enrolled past the 14 day free trial (made a payment) divided by the number of unique cookies that clicked on the "start free trial" button. The number of payments can be affected the experiement and retention values; therefore this will be used as an evaluation metric.

* **Net conversion:**  The number of user-ids to remain enrolled past the 14 day free trial (made a payment) divided by the number of unique cookies that clicked on the "start free trial" button. The number of payments can be affected by the experiment and as a result the net conversion, this will be used as an evaluation metric. There should be a statisticial significant increase in payment/continued enrollment after the free trial.


### Measuring Standard Deviation
**Analytical Estimate of Standard Deviation of Evaluation Metrics**

Evaluation Metric|Standard Deviation 
-|-
Gross Conversion|.0202 
-|-
Retention|.0549 
-|-
Net Conversion|.0156 
-|-

<br>
The number of clicks and enrollments both follow a binomial distribution. The standard deviation is computed with - sqrt(p(1-p)/n)

The standard deviation calculated for each sample has a size of 5000 unique cookies visiting the course overview page. Please see Baseline Values - the standard deviations are calcuated using these [baseline values](https://docs.google.com/document/u/1/d/1aCquhIqsUApgsxQ8-SQBAigFDcfWVVohLEXcV6jWbdI/pub?embedded=True).

Based on the 3 evaluation metrics, the analytical standard deviation will likely match the empirical standard deviation as the units of diversion for the experiment and analysis is cookies. While for the metric retention, given that the units of diversion and analysis are different (user-id vs cookies), it is likely that the analytical standard deivation and the emperical standard deviation will not match.

### Sizing
**Number of Samples vs. Power**
The Bonferroni Correction was not used during the analysis phase. The number of page views required (largest sample size) to conduct this experiment is: 4,741,212

Metric|Pageviews
-|-
Gross Conversion|646,450
-|-
Retention|4,741,212
-|-
Net Conversion|685,325

**alpha value of 0.05 and beta value of 0.2 is used**

**Duration vs. Exposure** <br>
Given the low risk and lack of sensitive data being collected, I would divert 100% of the traffic. With approx. 40,000 page views per day, the experiment would take roughly 119 days. However, this time period is too long to conduct an experiment for Udacity. Revising my previous decision, retention will no longer be used as an evaluation metric.

New evaluation metrics are Gross Conversion and Net Conversion. The new number of page views required is 685,325 and the experiment will now require 18 days to complete. Note that if other experiments need to be conducted simutaneously, the percentage diversion can be reduced.

Metric|Duration
-|-
Gross Conversion|17
-|-
Retention|119
-|-
Net Conversion|18

## Experiment Analysis
[Control and Experiment data](https://docs.google.com/spreadsheets/d/1Mu5u9GrybDdska-ljPXyBjTpdZIUev_6i7t4LRDfXM8/edit#gid=0) provided by Udacity and used throughout this section.

### Sanity Checks<br>
Below is the computed 95% confidence inteval for the listed invariant metrics

Invariant Metric|Lower Bound|Upper Bound|Observed|Pass/Fail
-|-|-|-|-
Number of Cookies|.4988|.5012|.5006|Pass
-|-|-|-|-
Number of Clicks|.4959|.5041|.5005|Pass
-|-|-|-|-
Click-through Probability|.0812|.0830|.0822|Pass

### Result Analysis
**Effect Size Tests** <br>
Below is the computed 95% confidence interval around the difference between the experiment and control groups.

Evaluation Metric|Lower Bound|Upper Bound|Statisticially or Practically Significant
-|-|-|-
Gross Conversion|-0.0291|-0.012|Yes (statisticially and Practically)
-|-|-|-
Net Conversion|-0.0116|.0019|No (statistically and Practically)

**Sign Tests** <br>
Below is the computed sign test using the day-by-day data.

Evaluation Metric|p-value|Statistically Significant
-|-|-
Gross Conversion|0.0026|Yes
-|-|-
Net Conversion|0.6776|No

## Summary
An experiment was conducted in which potential Udacity students were diverted by cookie into two groups, experiment and control. The experiment group was asked to input the amount of time they are willing to devote to study, after clicking a "start free trial button", whereas the control group was not. <br><br>
Three invariant metrics (`Number of Cookies`, `Number of clicks on "start free trial"`, and `Click-Through-Probability`) were chosen for purposes of validation and sanity checking while `Gross Conversion (enrollment/cookie)` and `Net Conversion (payments/cookie)` served as evaluation metrics. <br><br>
The null hypothesis is that there is no difference in the evaluation metrics between the groups, futhermore, a practical signifcance threshold was set for each metric. The requirement for launching the experiment is that the null hypothesis must be rejected for all evaluation metrics and that the difference between branches must meet or exceed the practical signficance threshold. Because our acceptance criteria requires statiscally signifcant differences for all evaluation metrics, the use of the Bonferonni correction is not appropriate. 
>The Bonferonni correction is a method for controlling for type I errors (false positives) when using multiple metrics in which relevance of any of the metrics matches the hypothesis. In this case the risk of type I errors increases as the number of metrics increases (signifcance by random chance). In our case in which all metrics must be relevant to launch, the risk of type II errors (false negatives) increases as the number of metrics increases, so it stands to reason that controlling for false positives is not consistent with our acceptance criteria.

Analysis revealed the expected equal distribution of cookies into the control and experimental groups, for the invariant metrics, at the 95% CI. A difference in gross conversion was found to be statistically signficant at the 95% CI, and the null hypothesis was rejected. Gross conversion also met the practical signficance threshold. Net Conversion was found to be neither statistically nor practically signficant at the 95% CI.

## Recommendation
This experiment was designed to determine whether filtering students as a function of study time commitment would improve the overall student experience and the coaches' capacity to support students who are likely to complete the course, without significantly reducing the number of students who continue past the free trial. A statistically and practically signficant decrease in Gross Conversion was observed but with no significant differences in Net Conversion. This translates to a decrease in enrollment not coupled to an increase in students staying for the requisite 14 days to trigger payment. Considering this, my recomendation is **not to launch**, but rather to pursue other experiments.

## Follow-up Experiment
The construct of student frustration could be assigned an operational definition of "cancel early," where a convenient definition and measure of early cancellation is prior to the end of the 14 day trial period in which payment is triggered. An early cancellation is not necessarily indicative of frustration but could be from other causes, such as a course not being aligned to the students needs or expectations in terms of content. For preventng early cancellation there are two primary logical timepoint opportunities for intervention, (1) pre-enrollment, and (2) post-enrollment but pre-payment.

The first opportunity for intervention was explored above wherein a poll regarding time commitment was used as to filter out students likely to become frustrated. This filter focused only on time commitment to the class and did not address other reasons why a student might become frustrated and cancel early. Even if the student was sincere in their response and dilligent in their study, they may become frustrated if they don't have the suggested pre-requisite skills and experience. That is, their committed time may not be enough if they don't come in with the pre-requisite skill set. Adding a checklist of pre-requisite skills to the popup regarding time commitment may be informative. This experiment would leverage the infrastrucure and data pipeline of the original experiment and be set up in the same way as the original, including the unit of diversion. The only difference would be the information in the form. If the student's answer meets the time and pre-requisite requirements (radiobox checklist) they are directed to enroll in the free trial, otherwise they are encouraged to access the free version. This experiment would be low cost in terms of resources and may increase the selectivity of the pre-enrollment filter. A succesful experiment would be one in which there is a signficant decrease in Gross Conversion coupled to a significant increase in Net Conversion.

A variety of approaches could be used to intervene post-enrollment but pre-payment and could be deployed concurrently with pre-enrollment intervention. An ideal approach would be one which minimizes the use of additional coaching resources to best meet the original intent of the intervention. An effective approach may be to employ peer coaching/guidance by means of team formation. If a student has a team of other students which they could consult, discuss coursework and frustrations with, and be accountable to, they may be more likely to stick out the growing pains and stay for the long term. The experiment would function in the following manner.

**Setup:** Upon enrollment students will either be randomly assigned to a control group in which they are not funnelled into a team, or an experiment group in which they are.

**Null Hypothesis:** Participation in a team will not increase the number of students enrolled beyond the 14 day free trial period by a significant amount.

**Unit of Diversion:** The unit of diversion will be user-id as the change takes place after a student creates an account and enrolls in a course.

**Invariant Metrics:** The invariant metric will be user-id, since an equal distribution between experiment and control would be expected as a property of the setup.

**Evaluation Metrics:** The evaluation metric willl be Retention. A statistically and practically significant increase in Retention would indicate that the change is succesful.

If a statistically and practically signifcant positive change in Retention is observed, assuming an acceptable impact on overall Udacity resources (setting up and maintaining teams will require resource use), the experiment will be launched.
