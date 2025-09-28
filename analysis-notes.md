**Analysis Notes – Employee Survey

**Dataset**
- File: Employee Survey.xlsx
- Sheet: HR Survey Reponses
- Each row: one answer to one survey question

**Cleaning steps**
- Kept only rows with `Status = Complete`
- Removed `Response = 0` (Not Applicable)
- Trimmed spaces in Department names
- Set `Response` column as Whole Number

**Core measures (DAX)**
Total Responses = CALCULATE(
    COUNTROWS('HR Survey Reponses'),
    'HR Survey Reponses'[Status] = "Complete",
    'HR Survey Reponses'[Response] > 0)

Total Respondents (Completed) =
DISTINCTCOUNT(
    CALCULATETABLE(
        'HR Survey Reponses'[Response ID],
        'HR Survey Reponses'[Status] = "Complete"  ))

Completion Rate % =
DIVIDE([Total Respondents (Completed)],
       DISTINCTCOUNT('HR Survey Reponses'[Response ID]), 0)

Positive Responses =
CALCULATE([Total Responses],
    'HR Survey Reponses'[Response Text] IN {"Agree","Strongly Agree"})

% Positive =
DIVIDE([Positive Responses], [Total Responses], 0)

Avg Score =
AVERAGE('HR Survey Reponses'[Response])

**Dashboard layout**
**Top row (Cards)**
Total Responses
Valid Responses
Total Employees
Average Score
% Positive

**Middle row:**

Avg Score by survey question

Avg Score by Job Level

**Bottom row:**

Depat avg scores, % rates
Heatmap (Matrix): Department × Question with background color red→green
