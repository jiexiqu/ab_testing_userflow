# A/B Testing - Deciding the Effectiveness of Adding Screener in User Flow on Decreasing Early Course Cancellation

## Experiment Overview
Experiment is conducted by Udacity, a website focusing on online courses. The business goal is to maximizing course completion by their users/students. 

**Control - Before Treatment/Change**
- At time of the experiment, Udacity courses have two options on the course overview page: 'start free trial', and 'access course materials' 
- When student clicks 'start free trial', they will be asked to enter credit card information, and they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first.  
- If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

**Experiment - Description of the Treatment/Change**
- The change was that if the student clicked "start free trial", they were asked how much time they had available to devote to the course. 
- If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. 
- If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. 
- Student have the option to continue enrolling in the free trial, or access the course materials for free instead. 
- [Screenshot](https://drive.google.com/file/d/0ByAfiG8HpNUMakVrS0s4cGN2TjQ/view?usp=sharing) of what the screener/experimnet looks like.

**Logic Behind the Change**
- The hypothesis was that the addition of the screener would set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enought time - without significantly reducing the number of students to continue past the free trial and eventually complete the course. 
- If the hypothesis is true, Udacity could improve the overall student experience and improve coaches' capactiy to support students who are likely to complete the course. 

## Experiment Design

**Unit of diversion (provided by Udacity)**
Unit of diversion is a cookie, but if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.

**Metric Choice**
For an a/b testing experiment, we need to define two types of metrics: invariant and evaluation metrics. 

*Invariant metrics* are metrics that should not change cross the experiment & control groups. These metrics are used for "sanity checks" - that is, using the it to check if the experiment setup and results make sense.
In this experiment, we have choosen the following to be the invariant metrics:
- Number of cookies: The number of unique daily cookies to view the course overview page. This invariant metric is the unit of diversion, and is expected to similar for the control and experiment groups. 
- Number of clicks: The number of unique daily cookies to click the 'start free trial' button (which happens before the free trial screener). This is a good invariant metric because at this point in the user funnel, all users still have the same experience so the experiment should not have any impacts on this metric - meaning both groups should have similar values for this metric. 
- Click-through-probability: Number of unique daily cookies to click the 'start free trial' button divided by number of unique cookies to view the course overview page. Again, all user experiences are still the same for both groups at this point, thus, metric cannot be impacted by the treatment. 


*Evaluation metrics* are the metrics that are expected to change across the treatment and control groups. For each metric, there is a predetermined minimum difference (dmin) that serve as a practical significance to the business - basically, it is the minimum change that must be observed for consideration in launching the experiment. 
The following are the choosen evaluation metrics:
- Gross conversion: Number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the 'start free trial' button. For this metric, we expect the treatment group to be lower than that of the control group. Through the treatment, we expect to redirect students who don't have enough time to study - thus not a good fit for the paid version, to the free version.  
- Retention: Number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. For this metric, we expect it to increase for the treatment group since we filtered out students who are likely to churn via the screener. 
- Net conversion: Number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the 'start free trial' button. For this metric, we hope to observe an increase for the treatment group, but this will all depend on the gross conversion and retention. 

The following tables serve as a summary of the choosen metrics. 

| Invariant Metric Name | Definition/Formula | dmin
| ------------- | ------------- | ------------- | 
| Number of Cookies (C)  | # of unique daily cookies to view course overview page  | 3000  |
| Number of Clicks (CL)  | # of unique daily cookies to click the 'start free trial' button |  240  |
| Click-Through-Probability (CTP)  | # of clicks/# of cookies  |  0.01  | 

| Evaluation Metric Name | Definition/Formula  | dmin  |
| ------------- |-------------| -----|
| Gross Conversion (GC) | # of user-ids enrolled/# of clicks | -0.01 |
| Retention (R)   | # of user-ids that paid/# of user-ids enrolled  |  0.01 |
| Net Conversion (NC) | # of user-ids paid/# of cookies    |   0.00075 |
