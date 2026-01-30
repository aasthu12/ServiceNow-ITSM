## Key DAX Measures

### MTTR (Days)
AVERAGEX(
    FILTER(
        Incidents,
        NOT ISBLANK(Incidents[Resolved_At])
    ),
    DATEDIFF(
        Incidents[Opened_At],
        Incidents[Resolved_At],
        DAY
    )
)

### SLA Met %
DIVIDE(
    CALCULATE(
        COUNT(Incidents[Incident_Number]),
        Incidents[SLA_Status] = "Met"
    ),
    COUNT(Incidents[Incident_Number])
)

### Incident Aging (Days)
DATEDIFF(
    Incidents[Opened_At],
    TODAY(),
    DAY
)

### Incident to Change % 
DIVIDE(
    [Incidents with Changes],
    [Total Incidents]
)

###Emergency Changes 
CALCULATE(
    COUNT('changes'[Change_Number]),
    'changes'[Change_Type] = "Emergency",
    NOT ISBLANK('changes'[Linked_Incident])
)

###Backlog Incidents 
CALCULATE(
    COUNT('incidents'[Incident_Number]),
    ISBLANK('incidents'[Resolved_At])
)

###Average Change Duration (Days) 
AVERAGEX(
    FILTER('changes', NOT ISBLANK('changes'[Closed_At])),
    DATEDIFF('changes'[Opened_At], 'changes'[Closed_At], DAY)
)
