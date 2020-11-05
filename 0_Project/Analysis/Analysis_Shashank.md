# Taxis Strike Back – Analysis

## Content  

### Core questions  

- **What problem is addressed?**
	- Taxi fleets operators world-over have been facing intense competitions from various ride-hailing services such as Uber or Grab (specific to Asia) 
- **Is it an important problem?**
	- From a socio-economic perspective, addressing this problem is important as ride-hailing services monopolise the industry, the taxi drivers will be at the ride-hailing services mercy. By addressing this problem, the power is given back to the taxi fleets in a sustainable manner and hence the name of the paper "Taxis strike back".
- **What approach has been taken to address this problem?**
	- A ***'Driver Guidance System'(DGS)*** is developed by this research team which is a real time system made of the following sub-components -
		- **Data stream handler**: Containig real time GPS coordinates, states (Available, booked, offline or something else). All the taxi locations are mapped continuously to physical roads using HMM based map matching algorithm.
		- **Demand and supply prediction engine**: The main innnovation in the design of the demand prediction engine is to treat each free-crusiing taxi as a 'demand probe'. Independent prediction models for all tuples (road link, day of week, time of day) are developed. The models return the likelihood of a taxi getting a trip. The engine uses a multilevel logistic regression model to estimate the aforementioned likelihood. By monitoring taxi movements in real time, we can utilise the regression model and predict the likelihood of taxi demands along all links. With historical data of taxis, the demand counts are predicted through simulation and then the expected demands are generated.
		- **Multi agent recommendation system**: This generates personalised recommendations for all taxi drivers based on their location with the objective of balancing overall demands and supplies across the city. In this context, this problem is viewed as a specialised spatio-temporal matching problem where taxis as agents are instructed to move around and match with stationary passengers. The group solve this problem with multi agent matching problem using a centralised multi period stochastic optimisation model. Without getting into the math of the solution, the goal is to calculate an optimal matching for all drivers such that demand fulfillments and movement costs are balanced over the planning horizon. As adaption of this system is quite difficult, the system handle such situations by simulating behaviours based on historical cruising patterns (made available by LTA). When performing demand assignments in the optimisation model, the part of demand fulfilled by drivers not using GDS is explicitly considered.
		- **Mobile application**: There's an app. Not focusing too much on this.
- **What (main) results and insights have been achieved?**
	- To gain insights, the following measurements are captured:
		- Estimated roaming time it takes a driver to acquire a trip
		- If the acquisition of a trip can be attributed to DGS guidanace.
	- By incorporating 20k taxis, it is shown that high-quality decision supports can be genrated for taxi drivers by integrating a dunamci demand prediction engine and a multi agent, multi period (I think this means different times of the day) optimisation engine.
	- To the best of their knowledge, this is the first operating guidance system for taxi drivers that combines real time data analytics and high performance multi agent optimisation.

### Information to be covered

To explain most parts of the paper there is sufficient information available in the paper itself. Unfortunately for us, there isn't sufficient information (within the paper) about their multi agent recommendation system. Since our focus should be on this, additional work will have to be done in this area of the paper.

## Critics

### Important Hints for Presenters and their Audience  

- **Paper structure**:
	- Overall the paper is well structured. There are a couple of things that are either informed at a very late stage of the paper or completely missed. For example -
		- The reason for fall in taxi ridership is explained at a very late stage of the paper (in the field trial section to be precise). The problem statement needs to incorporate this in particular.
		- There isn't sufficient background on how taxi system is setup in Singapore and how private cars were allowed for hire with the entry of Uber and Grab. Every country has different regulations for providing such services. I personally think it is important that this background is provided for a global audience.
		- Another thing to be highlighted is - how did the end user sign up for this trial? Not the taxi drivers but people requesting for the taxi service. Still not clear how they ended up being part of this trial.
- **Writing style? (clear and understandable)**:
	- IMO, it is pretty clear about all the information provided and well written.
- **Reasonable approach?**
  - *Why?*
  	- Based on my limited knowledge of agents and multi agents, this seems like a reasonable approach with simulation for evaluation.
  - *Why not?*
  	- I'm not sure if I can answer this at the moment, as the knowledge on this is still limited. 
  - *Could it be improved?*
  	- Need to do more research 
- **Experiments conclusive, convincing, waterproof, complete, reproducible?**
	- Yes, I think so. 
- **Claims are connivingly addressed and backed with (theoretical, experimental) results?**
	- Yes.	
- **Assumptions are clearly identified, any implicit assumptions?**
  - *Assumptions are reasonable?*
	  	- I don't think any assumptions have been made as they also do a field trial.
  		- The other interesting thing is that they even highlight the errors that might occur. 
  - *Realistic?*
  		- Yes 
  - *Oversimplified to the original problem?*
  		- I don't think so.
- **Any novel applications?**
	- Unsure. 
- **Follow-up research recommendation?**
	- Alternate approaches need to be identified for comparison. 
- **Anything unclear to you?**
  - *What did you miss?*
  		- Multi agent recommendation engine in detail. 
  - *Experiments with specific parameter settings*
		- Pretty clear 
  - *Comparison to other approaches*
  		- Need to do this.
  - *Critical discussion by the authors*
  		- Not sure if this is done. 

### Evaluation Points given by the assessment rubric  

- **Research work is well motivated?**
	- Yes 
- **Key contributions**
	- Provisioning alternate option to Uber/Grab for taxi fleets while still having an optimised system.
	- Major innovation in the design of the demand prediction engine is to treat each free cruising taxi as a demand probe.
- **Relevance/importance**
	- Pretty relevant in a socio economic context.
	- Scientific - I'm unsure.
- **Assumptions**
	- Adaptation by end user (Users who book the taxi service)
	- Adaptation by a large taxi fleet even whilst providing benefits.
- **Limitations**
	- Don't know any.
- **Own views on future research prospects**
	- None	
- **Strengths**
	- Well structured, easy to understand, adds value 
- **Weaknesses**
	- Additional background information is required. 
