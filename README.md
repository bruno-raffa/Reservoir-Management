# Reservoir Management
Water reservoir levels must be carefully controlled to satisfy consumer demand while maintaining minimum water levels. To satisfy this demand and maintain at least a minimum level of water in the reservoir, pumps can be operated to provide water flow into the reservoir. To operate these pumps there is a cost, and we would like to choose which pumps to use throughout the day in order to minimize cost.

In this demo scenario, we have seven pumps that can be operated on 1-hour intervals throughout a 24-hour day.

The approach used here involves the use of a Constrained Quadratic Model (CQM) from Dwave (https://cloud.dwavesys.com/). The solution is computed using the LeapHybridCQMSampler. The results obtained with this model show a better performance (in terms of minor operating cost of the pumps), if compared with the BQM used by the authors

### Objective

TThe general objective for this problem is to minimize cost. Cost is determined by which pumps are used in each time slot. To compute the cost for a given time slot, we must take into consideration the amount of power required for each pump in use as well as the cost of power at the given time. The cost per unit of power changes at different times of day, meaning that the cost to operate a pump also varies at different times of day.  We can formulate this objective mathematically as: min Σt Σp ct,p xt,p

where the summations are over time slots t and pumps p, and c(t,p) is the cost to operate pump p at time slot t.

### Constraints

1. Each pump must be used at least once. This allows us to use pumps routinely so that they do not fall into disrepair. Mathematically, this constraint can be written as Σt xt,p ≥ 1, for each pump p.

2. Each time slot must have at least one unused pump as a backup. Mathematically, this constraint can be written as Σp xt,p ≤ |P| - 1, for each time slot t.

3. At each time slot, the water level must be within allowable levels. To more clearly represent this constraint mathematically, we introduce a placeholder variable vi that represents the reservoir water level at time i. For the first time slot, we define v1 = Σp fpx1,p + Vinit - d1, where fp is the flow of pump p, Vinit is the initial reservoir water level, and d1 is the consumer demand in time slot 1. For time slots after time slot 1, we define
vi = Σp fpxi,p + vi-1 - di. At any given time slot t, we must enforce the constraint that Vmin ≤ vt ≤ Vmax.

### User Inputs
Number of pumps
Time steps (hours)
Pumps power
Hourly cost of electricity
Pumps flow rate
Water demand per hour
Water levels (initial, min, max)

### Output
Table representation of activated pumps per hour
Total flow
Total cost

## References
Kowalik, Przemysław, and Magdalena Rzemieniak. "Binary Linear Programming as a Tool of Cost Optimization for a Water Supply Operator." Sustainability 13.6 (2021): 3470.
