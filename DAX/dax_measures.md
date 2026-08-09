# DAX Measures

## Core Measures

```DAX
Total Student Counts =
DISTINCTCOUNT('Student Details'[Student_ID])
```

```DAX
Avg Sleep Hours =
AVERAGE('Student Details'[Sleep_Hours_Per_Night])
```

```DAX
Avg Usage Hours =
AVERAGE('Platform Details'[Avg_Daily_Usage_Hours])
```

```DAX
% Affected Academically =
DIVIDE(
    CALCULATE(
        COUNTROWS('Platform Details'),
        'Platform Details'[Affects_Academic_Performance] = "Yes"
    ),
    COUNTROWS('Platform Details')
)
```

## Recommended additional portfolio metrics

```DAX
Avg Addiction Score =
AVERAGE('Student Details'[Addicted_Score])
```

```DAX
Avg Mental Health Score =
AVERAGE('Student Details'[Mental_Health_Score])
```

```DAX
Avg Conflicts =
AVERAGE('Student Details'[Conflicts_Over_Social_Media])
```

```DAX
Students Affected Academically =
CALCULATE(
    DISTINCTCOUNT('Platform Details'[Student_ID]),
    'Platform Details'[Affects_Academic_Performance] = "Yes"
)
```

```DAX
% High Addiction =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT('Student Details'[Student_ID]),
        'Student Details'[Addicted_Score] >= 7
    ),
    [Total Student Counts]
)
```

> Threshold-based measures should be aligned with the business definition used in the final report.

