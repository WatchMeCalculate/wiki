Aperiodic Jobs
==============

Unpredictable jobs

- Periodic jobs have higher priority so they don't miss deadlines
- Better user experience if Aperiodic jobs get scheduled sooner

- Use FIFO queue

Slack Stealing
- You can rearrange schedule for periodic jobs as long as periodic jobs meet deadline


### Sporadic Jobs

- Unpredictable, but have hard deadline
- Parameters of sporadic jobs are known
- Can be given a priority

#### Acceptance Test

- Will it meet deadline?
- If not, can periodic tasks be rearranged so that it will
- In order to know if a sporadic job can be accepted we must calculate the slack between frame _i_ and _i'_
 - where i = [t/F] and k = [d/f] - 1 is the last full stack

##### Example

Frame size is 4
4 sporadic jobs

|  | ri | ei | Di |
------------------
|S1| 3 | 4.5 | 17 |
|S2| 4.5 | 4 | 29 |
|S3| 11 | 1.5 | 22|
|S4| 14.5 | 5 | 44|

for each job calculate the slack time . For job 1 scheduling starts in frame 2, must complete by frame 4. Total slack of the system is 4 so scheduler rejects it

### Deferrable Server Theory

Background poller task, this speeds up response time of aperiodic job

#### Assumptions

 - Pre-emptible
 - Independent
 - Feasible schedule for periodic tasks
 - Minimize response time for aperiodic jobs

#### Server Rules

 - *Consumption Rule* rule describing when and how much of the budget is decreased when the server is executing
 - *Replenishment Rule* rule describing when and how much the budget is increased


 #### Urm formula designing the server

 1. Calculate the U for the whole system without server
 2. Choose Ps and Es and consider es/ps = Us
 3. Calculate U + Us. This must be less than Urm. if not select new params for Ps and Es
 4. the ration between Ps and es determines server utilization

##### Example

System with three periodic tasks, T1 (3,0.5) T2 (20, 5) T3(60, 10)
U = 0.5/3 + 5/20 + 10/60 = 0.583

add server to Urm formula

Urm(4) = 4(2^(1/4) - 1) = 0.757
U + Us <= 0.757
Us <= 0.174

We select Ps = 9 and es = 1.5
This gives 0.583 + 0.167 = 0.7497

We can the do time demand analysis to determine feasibility



