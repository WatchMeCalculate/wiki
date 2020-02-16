Dynamic Scheduling
=================

 Utilization test nor Urm test can verify feasibility in case utilization is between urm and 1


### Short Response Time Theory

Consider tasks with response time equal or at most their period
#### Critical Instant
- The time interval where the job in Ti is released.as the maximum response time of all the jobs ever released in Ti
- If the job meets the deadline, all jobs will meet the deadline
- Maximum response time of a job in Task Ti is defined as Wi

##### Example:
 given Two tasks T1,(4, 1) and T2(5, 2) both were schedule with RM
 Critical instant of T2 at time t=15 is 3 because T2 is interrupted by T1 and then again switches back to T2 at time 17. This is where we scheduled the longest job

#### Time Demand analysis
Can be used if:
 - Using RM scheduler
 - Pre-emptible tasks
 - One processor
 - No Phases or jitter
 - A set of only periodic jobs

Highest priority task is determined by the period

|  | P | e | D |
----------------
|T1| 2 | 1 | 2 |
|T2| 3 | 1 | 3 |
|T3| 6 | 0.5 | 2 |

Wi(t) = ei + Sum((t/pk)ek)
W1(1) = 1 + 0 = 1
W1(2) = 1 + 0 = 1

W2(1) = 1 + 1/2 * 1 = 2.0
W2(2) = 1 + 2/2 * 1 = 2.0
W2(3) = 1 + 3/2 * 1 = 3.0

W3(1) = 0.5 + 1/2 * 1 + 1/3 * 1 = 2.5
W3(2) = 0.5 + 2/2 * 1 + 2/3 * 1 = 2.5
W3(3) = 0.5 + 3/2 * 1 + 3/3 * 1 = 3.5
W3(4) = 0.5 + 4/2 * 1 + 4/3 * 1 = 4.5
W3(5) = 0.5 + 5/2 * 1 + 5/3 * 1 = 5.5
W3(6) = 0.5 + 6/2 * 1 + 6/3 * 1 = 5.5


### Dynamic Priority Scheduling

- Adapts to the need of CPU for tasks during run time.
- When a task comes closer to it's deadlines, priorities can dynamically increase to make the task not miss the deadline
- Non-optimal schedule can occur compare to static scheduling
 - Under utilization

#### Dynamic Evaluation

- Priorities are reassigned based on the scheduler algorithm
  - Time left until deadline
  - The period
  - The slack time left
  - The release time

#### DP algorithms

- Least Slack Time scheduling
  - Slack of a job _i_ at time _t_ is defined as  si = di - t - e'i
    - dt is the deadline
    - t is the current time
    - ei is the remaining execution time of the job
    - if job has not been executing the e'i = ei
  - High utilization

- EDF - Earliest deadline first
  - Advantages
    - Very flexible
    - moderate complexity
    - Able t handle aperiodic jobs
  - Disadvantages
    - Optimality requires preemptive jobs
    - Not optimal on several processors
    - Difficult to verify


