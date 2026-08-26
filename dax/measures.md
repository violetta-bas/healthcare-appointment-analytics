# DAX Measures

This file contains the key DAX measures used in the Healthcare Appointment Analytics dashboard.

### Total Appointments

```DAX
Total Appointments =
COUNTROWS(FactAppointments)
```

### Distinct Patients

```DAX
Distinct Patients =
DISTINCTCOUNT(FactAppointments[PatientID])
```

### No-Show Rate

```DAX
No-Show Rate =
DIVIDE(
    [No Show Count],
    [Total Appointments],
    0
)
```

### 15+ Days No-Show Rate

```DAX
15+ Days No-Show Rate = 
CALCULATE(
    [No-Show Rate],
    FactAppointments[LeadTimeCategory] = "15+ Days"
)
```

### Pediatrics No-Show Rate

```DAX
Pediatrics No-Show Rate = 
CALCULATE(
    [No-Show Rate],
    DepartmentDim[Department] = "Pediatrics"
)
```

### Average Lead Time Days

```DAX
Average Lead Time Days = 
AVERAGE(FactAppointments[LeadTimeDays])
```

### Rolling 30-Day Appointments

```DAX
Rolling 30-Day Appointments = 
CALCULATE(
    [Total Appointments],
    DATESINPERIOD(
        CalendarDim[ApptDate],
        MAX(CalendarDim[ApptDate]),
        -30,
        DAY
    )
)
```















