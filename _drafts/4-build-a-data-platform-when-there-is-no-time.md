Management saying "I need this yesterday!" => not a cliché
Humanity is 10 years behind in terms of battery production - whether or not you think Batteries and electrification is part of our green future, it is at the moment the most promising solution.

that's the context
now how do you build a platform?


## Possible titles:
- "You don't have time to build an Analytics platform"
- Building analytics platforms when there is no time
- No time to build a data platform
- I need a data platform yesterday!


## Intro:

Typical management trope, but here there is some credit: Battery manufacturing in Europe is way behind what it should be to supply the demand.
There is literally "no time". Factories need to be built, to start and ramp up production now.
And these factories will produce data in the process, and this data is a valuable companion to adjust operations at all stages.

## Themes:
### Grow organically:
Start Small, grow continuously based on user needs.
A lot of platforms out there are built based on a vision that matches the business needs.
However in a context such as Northvolt, such vision, not matter how good it was, would have been wrong as the whole business itself changes rapidly.
Don't get me wrong, it is good to have a vision to give out a meaningful direction, however it needs to be broad enough to encompass the adaptability we eventually needed.

#### History
##### Phase 1:
"Open Manufacturing Data"
Athena + Superset (enable access to manufacturing data)
##### Phase 2:
"Self-Service Open Manufacturing Data"
Athena + Looker
+ More flexibility
+ Enables people to build their content themselves
##### Phase 3:
"Reporting Analytics for Manufacturing"
+ Higher performance
+ Higher availability 
+ Redshift + Looker (improve query performance and reliability)

#### Misc
Build ad-hoc extensions for use-cases that pushes the envelope too far
- Real-Time monitoring of simple values with Postgres + Grafana
- Real-Time Advanced Analytics with Flink


### Keep the users engaged

The data in an analytics platform has no value if it is not used. To bring people to use the data, it needs to solve concrete problems from day 1 of your platform.
People using the data will need to be kept in the loop to provide feedback and enable continuous improvement of your platform. 
If that means getting s*** on by the users because the data is wrong or the data is missing etc... then congratulations! You have user feedback!

But of course, we then need to demonstrate we take this feedback to improve.

### Walk the fine line between solve business issues and improve the platform

At all times there is this challenge of choosing between:
  - Working on solving a business need by building a specific dataset or dashboard
  - Working on Platform improvement and capabilities (change the technology, add tooling, monitoring etc...)

It is easy to spread your team too thin by chasing too many use-cases at the same time, and it is equally easy to lose user engagement by spending too much time on platform building.
This is where companies usually split the work between Analytics Engineers, and Data Platform Engineers, but they ultimately need to collaborate tightly to ensure fast deliveries and consistency in the data.
Given the context it is best to avoid splitting them into 2 teams as the lack of collaboration will create issues like:
- The analytics engineers implementing inefficient solutions
- The data platform engineers building capabilities that end up not being used

Both will slow everything down 

### Forget about what the vendors tell you
It is also easy to think about the usual suspects of data platforms like:
- Observability
- Cataloging
- Governance
- Self-Service or Data Mesh tooling

Unless these are business critical, they do not bring value in the short term, and should not be built before having a base data platform that works and is actively used.


### Conclusion




      
    