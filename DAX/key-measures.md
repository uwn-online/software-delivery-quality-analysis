# Software Delivery & Quality — DAX Measures

## Measure Summary

| Measure | Purpose |
|---|---|
| Releases | Total number of software releases |
| On-Time Release % | Percentage of releases delivered on schedule |
| Avg Delay Days (Late Only) | Average delay for releases delivered late |
| Automation % | Share of executed tests that were automated |
| Production Defects per Release | Average defects found after release |
| Production Incidents per Release | Average production incidents per release |
| Estimated Downtime Cost | Financial impact of service downtime |

---

## 1. Releases

Counts distinct software releases.

```dax
Releases =
DISTINCTCOUNT (
    'Release Performance Facts'[Release ID]
)
```

## 2. On-Time Release %

Calculates the percentage of releases delivered on or before their planned dates.

```dax
On-Time Release % =
DIVIDE (
    [On-Time Releases],
    [Releases],
    0
)
```

## 3. Automation %

Calculates the test-volume-weighted automation rate.

```dax
Automation % =
DIVIDE (
    [Automated Tests],
    [Tests Executed],
    0
)
```

## 4. Production Defects per Release

Calculates the average number of production defects per release.

```dax
Production Defects per Release =
DIVIDE (
    [Production Defects],
    [Releases],
    0
)
```

## 5. Production Incidents per Release

Calculates the average number of production incidents per release.

```dax
Production Incidents per Release =
DIVIDE (
    [Production Incidents],
    [Releases],
    0
)
```

## 6. Estimated Downtime Cost

Calculates downtime cost using each product/module's cost per minute.

```dax
Estimated Downtime Cost =
SUMX (
    'Release Performance Facts',
    'Release Performance Facts'[Downtime Minutes]
        * RELATED ( Product[Downtime Cost per Minute ($)] )
)
```
