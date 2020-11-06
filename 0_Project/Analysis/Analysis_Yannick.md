-What problem is addressed?
+ Overall problem is helping taxis stay competitiv in regard to uber and co
	Is it an important problem?
	+ It is an important problem. The taxi drivers have to pay many fees and  are obligated to many regulations. The uber driver do not have that which gives them a major advantage.
	+... uber driver can offer better prices and drive taxis out of business. It is a recognized problem, otherwise a lot of countries would not have banned uber all along.
	
	
	
-What  approach  has  been  taken  to  address  this  problem?
  (e.g.,  new  method  is  proposed, theoretical analysis, experiments, interviews, etc.)
 +DGS 
  + Data stream handler
	+ Issues: GPS errors(location discontinuity, out of bound errors, null signal)
	+ Data cleaning(errors above)
	+ Matching gps to streets (Hidden-Makrov-Model-based map-matching algorithm[10]) / rolling horizon manner? trajectories for all taxis independently
  + deamand and supply prediction
	+ each taxi as demand probe? Demand in a place inversly correlated to time passed since last visit
		+ Issue: Invalidates memoryless Poisson arrival process property(common approach) means: that the need for taxis need to be independent from taxis onsite. which contraticts the above statement.
		+ Solution: multilevel logistic regrssion to estimate liklihood to find a passenger on a street at a certain time.P(T=1|delta_s)= logit^-1(alpha_s_t_d, beta_s_t_d * delta_s) (1) s = street, d = day of week, t = time (30 mins chunk) delta_s is independent variable time since last taxi visit on street s
			+ Issue: no prediction of "demand counts" only liklihood of a demand
			+ Solution: Simulation with historical data and calculated "expected" demands that would be generated
  + multi agent recommendations
	+ Objective balance demand/supply in the whole citty
	+ spatio-temporal matching problem, taxi = agents(moving around), passenger = to match(stationary)
		+ Solution: centralized multi period stochastic optimization model
			+ maximize (2): G= set of grid cells, D is number of demands samples considered for the optimization, T = time horizon, Cost_i_j = cost driving from Gi to Gj, R_i_d = net Revenue for serving demand d in G_i, x^t^k_i_d is a decision varibale that assigns agents in G_i to demand d at time t within sample k, u_i_j  number of unassigned taxis moving from G_i to G_j
			+ global function reflective of total revenue
			+ Issue: Some drivers don't like it and drive as they want, reflected by using common driving patterns(important for demand assignments)
			+ executed every minute with newest data, planning horizon is 30 minutes
  + mobile app
	+ no need of user interactions
		+ region mode (highlight the region the driver should drive to)
		+ street mode (streets are highlighted according to probability of demand)


	



-What (main) results and insights have been achieved?
	+empirical results
		excluded airport trips
		oerall 21,5% less roaming
		only around 10% dgs compliance
		
	Implication that for every 10% dgs compliance the roaming time falls by 1,903 minutes

	+Spatial temporal breakdowns of DGS performance
		Workdays/ non workdays
		Central business district / non CBD
			works best 24-06 improvement 24-36
			non peak hours 10-17 nonCBD workday and CBD non workdday 17-19
			17-24 allreas and non work non cbd 15-17
			06-10 non wd non cbd 12%
		DGS good for sporadic and less perdictable areas


2nd Part

-Is the paper well structured?
	Is the writing style clear and understandable?
	+ Yes it is well structured. First the problem is addressed. Then a high level overview is given. Then the "modules" are explained. while explaining the modules a few issues are mentioned and how they are resolved
	+ I found the paper to be very understanble and well written
	
	+ Evaluation mention DGS percentage 5-100 twice
	+ Not sure if relevant
		30yo+ info to be taxi driver
		Infos about obstacle to drive taxis
		Big guy 50% rest split
		fleet size 28 k taxis 2015
		fleet size uber and co 42 k
		reduce taxi fleet to 24 k
		hire taxi driver for uber and co
		JustGrab mix of taxi / and private driver
	
	
-Is the approach proposed in the paper reasonable?
	Why, why not and how could it be improved?
	+ The problem is divided into 3 categories. Each category is nessecary and crucial to the outcome.
	+ Datastream handler seems like a general data cleaning/preparation task, which is nessecary with every data related projects. data stream handler:  The way the data is cleaned and matched to streets is not described. A lot of knowledge is required, for example they just mention the hidden makrov model but dont explain further. The GPS errors are mentioned but no explanation on how they are handled.
	+ demand and supply prediction: it is a prerequisite to understand logistic regression, would be to detailed to explain in the paper. The variables are explained and it makes sense.
	+ ma recommendations: the formula makes sense, and everything is explained. A verbose description of what (2) is doing would ve been nice
	
	

-Are the described experiments conclusive, convincing, waterproof, complete, reproducible, etc.?
	Evaluation
	+ Simulation with TaxiSim
			+ calibrated with real data
			+ 24 k taxis
			+ randomly generated passengers from profiles from real data
			+ variation of of use of DGS 5%-100%
			+ simulation provides streaming data like real API
			+ DGS calc from stream
			+ daily trips is key performance to look for
		+ Simulation shows  a decrease in efficency while the market share increases... nearly to the level of non guided. Still better than nonguided at every step
		+ Disagree: with the scaleabilitty of the system. If every taxi uses DGS there is nearly no benefit.
		+ Scalability doesn t change change amount of taxis?!
		+ No Uber and co considered. Could favourably change graph?!
	+ Field trial
		+Singapore
			1 month trials
			open recruitment
				for participation
					min 4 hours of usage
					100S$ incentive
				for compliance
					additional incentive percentage based up to  100S$
					can be tracked with app
			various registration infos
				age
				driving experience
				driving for uber and co
					estimate of those drives
			during trial info collected
				compliance
				usage <id, start, end>
				taxi trip related
					pickup from street
					pickup from booking (Does the booking pickup reset delta_s?!)
		+ analysis
			performance metric
				For driver most impoirtant  trips/hour (avg roaming time:= avgrt)
				Assumption: avg roaming time reflects driving skill
				trying to find out if DGS improves avgrt
				Find out if avgrt is due to dgs or not
				avgrt to find passenger
					check datastream to find time till state transition
						Street pick up state Available to Hired
						Booking state from Available to On-call to Hired
						Booking from app Available to Busy to hired
				Diagram to ilustrate how time is calculated
				DGS attribution is when pickup occures and driver is using DGS
					ratio calculated

				
						
		
		
	
-Are  all  claims  made  by  the  authors throughout  theirpaper (e.g., “we solve problem X“, “weextend method Yand ...”)
 backed upthrough theoretical and/or experimental results, that is, are allclaims convincingly addressed?
	+ there are no proofs, just simulations and field trials. Not sure wether proofs are needed as only proven methods are used
	



-Did   the   authors   clearly   identify   the   assumptions   they   made,   or   are   there   any   implicit assumptions not mentioned in the paper?
	Are these assumptions reasonable,
	are they realistic,
	or do they oversimplify the original problem?
		+ i am a little worried that 1 km x 1km is to coarse, but smaller grid will probably impact the performance.
		+ Implication that for every 10% dgs compliance the roaming time falls by 1,903 minutes
			this seems very unreliable... linear  regression. Simulation shows the more taxis use DGS the less effective it gets, this contradicts
	
	
-What novel applications might arise from the paper?
	+ Help Taxis organize from that. App is already available, This is more like an end product.
	+ DGS could be used for different fields


-What follow-up research do you recommend?
	+ Improve prediction algorithmn with other methods like transformers forecasting...
	+ Datastream Hanlder is basic architecture stuff and doesn t need more reasearch if it meets the requirements
	+ How the demand count is calculated
	+ Recommendation system, should stay planning problem and i don t think an ml approach is nessecary
	+ Should the airport wait time be added to the evaluation, can t cherry pick!


-What remained  unclear  to  you,  what  did  you  miss
  + How the data has been cleaned.
  + pickup from booking (Does the booking pickup reset delta_s?!)
  + What is the purpose of the region mode if street mode also shows region and probabillities of streets
