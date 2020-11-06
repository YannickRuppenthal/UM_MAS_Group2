# Taxis Strike Back – Analysis

## Content  

### Core questions  

- What problem is addressed?

This paper is about the results of a trial since 2017 with five months operational data
of "the" driver guidance system in Singapore which tries to make the taxi industry more
competitive against new highly technical competitors like uber.  

- Is it an important problem?
- What approach has been taken to address this problem?
- What (main) results and insights have been achieved?

### Information to be covered

Here stuff is covered I'd like to have included in the presentation besides the core questions.

#### Main critics of related work

1. Demand prediction is derived from historical GPS traces. 
2. Demand locally based on the current location of the taxi drivers which leads to greedy matching of demands and supplies. --> Crowded places

#### Main Goals (Or Problems to archive)

1. The chosen system must be reactive to the real-world data feed
2. consider the interaction among tens of thousands of taxi drivers.
3. scalable computationally  
    - execution time of the engine does not depend on the number of users.

#### DGS

**Data Stream Handler** takes GPS and status data, error corrects it and does Hidden-Markov-Model-based map-matching algorithm (HMMB MMA) to map to city model.  
**Demand and Supply Prediction Engine** uses a multilevel logistic regression model to to estimate a passenger on a street at different times.  
**Multi-agent Recommendation Engine** personalized recommendation with objective of balancing overall demands and supplies across the city.
The problem is a spatio-temporal matching problem.
Solution is a multi-period stochastic optimization model

#### Evaluation

Use a TaxiSim with history traces and let the agents behave based on the DGS.  
The simulation shows that DGS drivers always out-preform non DGS drivers

#### Field Trial

Its quite trival to boil that information down.

**Analysis**: If the specific fraction of the roaming time before a "service" (street pick up) was DGS guided then the service will be counted to be is responsible for the trip.

## Critics

### General critics

**Related work:** Is important because of the papers kind being about the deployment.  
Further the referenced work seems mostly distant to the actual work. 
E.g derive fast travel routs from taxi data... well that's not DGS and doesn't even try to do a recommendation for roaming..

**Field trip analysis:** Is mor like a presentation of data and less a interpretation.  
I would have liked a more thorough interpretation of general conclusions about the recommendations of the DGS .

### Important Hints for Presenters and their Audience  

- Paper structured?

Why are the main goals of the developed system written in the related literature?

- Writing style? (clear and understandable)

They try to be more elaborate then it actually needs to be.  
eg.
`We further break down the analysis by looking at the temporal and spatial dimensions.`
Basically meaning on what days and where does it work best.  

They assume to much knowledge of the reader about other DGS systems...  
> In other words, it invalidates the memoryless property of the exponential distribution and thus the demand will not follow the Poisson arrival process, which is commonly assumed in the literature.

- Reasonable approach?  
  - Why?  
  - Why not?  
I'm not sure how I feel about the compliance money incentives
  - Could it be improved?
- Experiments conclusive, convincing, waterproof, complete, reproducible?
- Claims are connivingly addressed and backed with (theoretical, experimental) results?

Looking at table 2 the amount of DGS Trips and Non-DGS trips is astonishing and raises the question how meaningful the data actually is.

- Assumptions are clearly identified, any implicit assumptions?  
  - Assumptions are reasonable?  
  - Realistic?  
  Well its a field trial... the assumptions are the reality..  
  The only thing to cricise is the incentive to use the application and the effects of saturation of the market in the real world. 
  - Oversimplified to the original problem?  
  Still kind of cant be because its the reality
- Any novel applications?

Well this is the novel application 😅  
But maybe let them pay you to use the app and not throw money at them to solve the problem.

- Follow-up research recommendation?
- Anything unclear to you?,
  - what did you miss  
  the memoryless property of Poisson arrival time? whut?
  - Experiments with specific parameter settings,
  - Comparison to other approaches  
    Were given but not to thoroughly explained why their approach is not suitable.  

  - Critical discussion by the authors  
There was none
  - Open questions  
  Why cant the competitors adapt similar technical approaches to combat the taxi industry and make this result basically meaningless?  
  It is not explained if the booking through the Grab or Uber app counts to be DGS guided.
  It is just explained how they differentiate between the two.

### Evaluation Points given by the assessment rubric  

- Research work is well motivated?

The purpose question basically boils down to `does the approach acctually work` which is a bit shallow for my taste.

- Key contributions
- Relevance/importance
- Assumptions
- Limitations
- Own views on future research prospects
- Strengths
- Weaknesses
