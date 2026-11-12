---
icon: lucide/chart-column-big
---

# 6. Statistics & Logging

Every action in MakeACS is logged and kept in perpetuity.The [history](./5-shop-management.md#history) page allows for searching for one-off information, such as identifying what user was using a piece of equipment at a specific time, or all MakeACS data can be accessed via SQL query for use with a larger system like Grafana, such as plotting average number of users per month. 

!!! info
    MakeACS logs can be kept for as long as there is server space to store them. See [system price](./7-system-price.md) for more information.

## Equipment/Space Data

Data on equipment, sign-ins, tool loans, etc. can all be used to identify trends in utilization. Collected data includes;

* Equipment session start time and duration
* Sign-in date and time
* Tool loan out and return times
* Time of, reason for equipment access denied

Below are some examples of this data in use;

Plotting sign-ins per day can help identify times of the year when the shops are more used, and may need more support.

![Image](./assets/makerspace%20swipes.png)

By averaging the number of sign ins per hour per day of the week, we can identify times of the day that may require more staffing;

![Image](./assets/users%20by%20hour.png)

Seeing if excessive numbers of access attempts are being denied, and if so for what reason, can help you understand if there is sufficient user training on how the system works.

![Image](./assets/stats%20access%20attempts.png)

## Training Data

Training data logged for analysis includes;

* Pass rate per training
* Correct rate per question in the training
* Datetime of training completion

This allows the identification of troublesome trainings and questions within them for refinement, or for identifying trends in training interests as a proxy for equipment interest. Exporting specific training results allows you to run reports on users who completed a training to allow it to be used as a class assignment. 

Training data is also collected in regards to staff, for instance being able to track how many in-person competency checks a staff performs, which equipment they perform the most in, etc.

## User Data

!!! tip
    Does your institution have specific policies regarding user data handling? No problem. MakeACS can be hosted by your institution directly to comply with regulations.

User data can be collected from [SSO attributes](./2-website.md#logging-in-sso), or collected manually from the user durning sign-up. Additional data is collected and associated with the user by MakeACS:

* Most recent sign-in
* Currently-used [theme](./2-website.md#customization)
* Sign-up date
* Most recent ID card update
* Completion datetime of trainings
* Usage of equipment

This user-centered focus on data allows you to develop narrative stories of the user's experience with the shop; did they start by coming in to use one piece of equipment then branch out as needed? Or did they plan ahead, complete all trainings on all equipment, then get to work?

## Website Data

Basic information related to the MakeACS website is logged, such as sign-up balks (a user started making an account, but gave up).

For more in-depth website usage data, MakeACS supports Google Analytics. Simply enter your tracking key to get real-time and historical data on traffic sources, popular pages, bounce rates, average time per page, and much more!