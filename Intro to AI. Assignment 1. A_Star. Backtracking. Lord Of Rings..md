# Algorithm Flow Description

## Backtracking algorithm:
The **Backtracking algorithm** explores all possible paths recursively while maintaining ring switching logic. For each move, it attempts to toggle the ring mode and updates switching permissions, ensuring safe movement by avoiding dangerous zones. It processes all neighboring cells within a Neumann zone (radius 1), preserving the original move mode state throughout recursive calls and restoring it upon completion to maintain consistency.

## A* algorithm:
The **A* algorithm** employs a heuristic approach using priority queues to navigate toward the most promising cells. It evaluates paths based on the cumulative cost from the start position plus Manhattan distance to the goal. Unlike backtracking, it doesn't explore all neighbors equally but selectively expands the most advantageous nodes. A path validation mechanism ensures connectivity by checking parent-child relationships, reconstructing the path through parent pointers when reaching intermediate nodes.

Both algorithms incorporate the same ring-switching mechanism that prevents entering hazardous areas and restricts ring toggling in life-threatening situations. This safety protocol ensures the agent never moves into danger zones or performs unsafe ring operations regardless of the pathfinding strategy employed.

# Statistical Analysis

Based on 1000 randomly generated test maps:
*\*win = found optimal path* 

| Algorithm    | Radius | Wins | Losses | Win Rate | Mean Time | Median Time | Std Time |
|--------------|--------|------|--------|----------|-----------|-------------|----------|
| A*           | 1      | 953  | 47     | 95.3%    | 0.164s    | 0.155s      | 0.054s   |
| Backtracking | 1      | 978  | 22     | 97.8%    | 0.921s    | 0.943s      | 0.341s   |
| A*           | 2      | 1000 | 0      | 100.0%   | 0.163s    | 0.151s      | 0.051s   |
| Backtracking | 2      | 1000 | 0      | 100.0%   | 1.334s    | 1.367s      | 0.352s   |

**Key Findings:** Backtracking achieves slightly higher success rate (97.8% vs 95.3%) for radius 1 but is significantly slower, taking approximately 5.6 times longer than A*. Both algorithms achieve perfect success with radius 2, though backtracking remains considerably slower. The consistent low standard deviation in A*'s execution time indicates more predictable performance compared to backtracking's higher variability.

# PEAS Description for Actor Agent
**Performance Measure:** Successful navigation to goal, minimization of execution time, avoidance of hazardous zones, efficient ring switching decisions.

**Environment:** Grid-based world with dynamic obstacles, ring-dependent zone accessibility, limited switching permissions, and time-sensitive constraints.

**Actuators:** Movement in four directions (up, down, left, right), ring mode toggling capability, path selection decision-making.

**Sensors:** Agents and hazard zones perception, goal location identification.

# Notable Observations
The analysis revealed several maps where both algorithms failed with radius 1, primarily due to unsafe navigation requirements. The limited perception range creates fundamental limitations - areas outside the agent's radius remain unknown, and ring switching in unexplored zones is prohibited due to lethal risks. This creates scenarios where pathfinding becomes impossible: the agent might be forced to wear the ring initially, but cannot determine when it's safe to remove it without venturing into unknown, potentially dangerous territory.

An interesting outcome worth highlighting is that while backtracking demonstrated marginally better success rates for challenging radius-1 configurations, its computational expense makes it impractical for time-sensitive applications. The perfect performance of both algorithms with radius 2 suggests that increased perception range significantly mitigates navigation challenges in this environment.

## Maps:

**Example 1:**

--- start-multi-column: ExampleRegion1  
```column-settings  
number of columns: 2  
border: disabled
shadow: off
```

*A\* with radius = 1*
After *(2, 0)* (or *(0, 2)*) keep ring putting on, so failed on *(0, 7)*
<br>

![500](Pasted%20image%2020251106080309.png)

--- end-column ---

*A\* with radius = 2*
Everything is okay, because agent knows *(3, 0)* and *(0, 3)* is safe, and he can switch the ring further.

![500](Pasted%20image%2020251106080342.png)


--- end-multi-column


















**Example 2:**
*A\* with radius = 1*
After *(0, 5)* continues not to wear the ring, so failed on *(0, 11)*

![500](Pasted%20image%2020251106082133.png)

*A\* with radius = 2*
Everything is okay, because agent knows *(0, 6)* is safe, and he can switch the ring further.

![500](Pasted%20image%2020251106082612.png)