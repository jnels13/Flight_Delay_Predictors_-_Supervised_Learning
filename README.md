# Flight Delay Predictors Using 2015 FAA Dataset

### Introduction

For the Mod3 Final Project, I used decision-tree and random-forest classifiers to determine which features were most important in predicting whether flights would be late.  I used the 2015 Flight Delays and Cancelations dataset from Kaggle (https://www.kaggle.com/usdot/flight-delays).  The dataset is very large, especially after it was one-hot encoded.  This was the largest challenge in the project, though using Google Colab Pro was a great resource.  

### Repository Contents

The files in the repository include the following: 
* <a href= "https://github.com/jnels13/Flight_Delay_Predictors_Supervised_Learning_Flatiron3.2.1/blob/master/index.ipynb"> index.ipynb </a> (the code)
* README.md (this file)
* <a href="https://github.com/jnels13/Flight_Delay_Predictors_Supervised_Learning_Flatiron3.2.1/blob/master/JLN%20Mod3%20Final.pdf">JLN Mod3 Final.key/.pdf </a> (the nontechnical presentation slides)

The dataset is too large to load into Github; it may be downloaded at the Kaggle link above. 

### Initial Review of the Data

Initial review of the dataset found 5,819,079 rows and 31 columns. The data were very clean and complete, though there were several columns which would not add to the analysis and were dropped. Additionally, the departure time feature was converted from continuous to a categorical variable composed of three-hour "windows." Additionally, the target, "arrival delay", was converted to a binary on-time/late, based upon a specific cut-off specified by the model user (the results below are based upon a zero-minutes-late threshold).

Review of the data with regard to flight delays (focusing on American airlines) shows that while American has the third-highest number of segments (takeoff-landing), its on-time performance is relatively good, with the third-least number of delays. However, when it has delays, they're longer than most other airlines.  Finally, instigators of delays are summarized on the last slide.

<img src="https://github.com/jnels13/Flight_Delay_Predictors_-_Supervised_Learning/blob/master/Tableau_Delays.gif" width="972" height="692">

### Methodology

The size of the dataset presented the most limiting factor. The data were very clean and complete, though there were several columns which would not add to the analysis and were dropped. Additionally, the departure time feature was converted from continuous to a categorical variable composed of three-hour "windows." Additionally, the target, "arrival delay", was converted to a binary on-time/late, based upon a specific cut-off specified by the model user (the results below are based upon a zero-minutes-late threshold).

Initial review found that there were several airports with only a single flight in or out in the one-year span of the dataset, so the airports were limited to only those designated as "Primary" airports by the FAA, for both arrivals and departures.  Similarly, I considered but rejected limiting the airlines in the model, considering their potential significance as predictors. Ultimately, I decided to limit the dataset to the first have of the year (Jan-Jun).  This reduced the datset enough to allow the models to run without too much delay. 

After one-hot encoding, I applied a decision-tree model and review the most important features. I then applied a random-forest model to the data, and again looked for the most important features. Finally, a GridSearch was formed to further tune the random forest, and the most important features were again 

### Results

As a disclaimer, these models will not predict a delayed flight with any great accuracy (the final testing accuracy was approximately 65%). However, it does give significant insight into which factors are more predictive of a delay. The initial decision tree showed the scheduled departure time to be the most significant feature in predicting delay. I looked at the three-hour windows in terms of delay, which lends some insight on the best (and worst) departure windows to choose: 

<img src="https://github.com/jnels13/Flight_Delay_Predictors_Supervised_Learning_Flatiron3.2.1/blob/master/Departuretime.png?raw=true" width="718" height="433">

Clearly, the 3am-6am departure window has the best on-time arrival performance, which then decreases through the day. Also in the initial model, Delta and Southwest Airlines were significant predictors (and to a lesser extent, Alaska Airlines, as well). Accordingly, I visualized the individual airlines' on-time performance as well:

<img src="https://github.com/jnels13/Flight_Delay_Predictors_Supervised_Learning_Flatiron3.2.1/blob/master/Airline.png?raw=true" width="920" height="533">

There are clearly airlines with better (Delta and Alaska) and worse (Frontier and Spirit) overall performance. Interestingly, neither of the bottom performers were important predictors with regard to these potential delays. 

As I developed the random forest, additional features emerged as "important": month of departure and airtime (length of the flight in the air). When visualizing these two features, there was not an obvious reason why month of departure was a significant predictor: 

<img src="https://github.com/jnels13/Flight_Delay_Predictors_Supervised_Learning_Flatiron3.2.1/blob/master/Month.png?raw=true" width="709" height="480">

There is no obviously significant variance in the delays over these six months, though on-time performance appears to improve in April and May.  The relationship between airtime and delays was more clear. Longer flights were much less delayed: 

<img src="https://github.com/jnels13/Flight_Delay_Predictors_Supervised_Learning_Flatiron3.2.1/blob/master/Airtime.png?raw=true" width="800" height="480">

Of these, airtime is the least "flexible," though travelers would be most likely to avoid delays by taking early morning flights, on Delta, in April or May.

### Further Work

The scope of this project was rather limited, and there are further questions to be considered, such as considering the day of the week, looking at how weather affected delays (which may play into why the months were significant predictors), and looking at the entire year's worth of flights. 


